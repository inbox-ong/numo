## NumoTrust: Autoridade Certificadora Root

No conceito de Infraestrutura Pública Digital (DPI), a confiança não é cega; ela é matematicamente validada minuto a minuto. O `NumoTrust` é a **Autoridade Certificadora (CA) raiz** interna do ecossistema e o guardião do *Zero-Trust Architecture*.

### 🎯 Responsabilidade
*   Atuar como Private PKI (Public Key Infrastructure) da rede estatal.
*   Emitir identidades e certificados dinâmicos (SPIFFE/X.509) para microsserviços internos.
*   Emitir e renovar certificados das Instituições Financeiras (IFs) participantes ligadas à rede externa.
*   Manter a lista de Revogação (CRL/OCSP) para interrupção de acesso imediata se um participante for comprometido ou bloqueado judicialmente.

---

### 🔌 API REST (Superfície de Conexão Externa/Interna)
A interação com o `NumoTrust` varia entre um processo pontual (onboarding de Instituição) e processos contínuos (renovação de curto prazo pelos agentes).

#### 1. Solicitar Certificado de Integração (CSR)
*   **Método:** `POST /v1/certs/sign`
*   **Quem chama:** Instituições da rede (via portal Admin) ou processos de automação autorizados.
*   **Payload:**
    ```json
    {
      "institution_id": "BANKABR1",
      "csr_pem": "-----BEGIN CERTIFICATE REQUEST-----\nMIIC...=\n-----END CERTIFICATE REQUEST-----",
      "requested_ttl": "72h" // Vida curta forçada para mitigar exfiltração de chaves
    }
    ```
*   **Respostas:**
    *   `201 Created`: Retorna as chaves assinadas se os critérios do CSR baterem prefeitamente com os dados do Directory.
    *   `403 Forbidden`: O "Institution ID" não tem *clearance* para assinar novos nós.

#### 2. Validação Contínua (Status OCSP/CRL)
*   **Método:** `GET /v1/certs/status/{cert_serial_number}`
*   **Uso:** Extensivamente utilizado pelo API Gateway a cada milissegundo.

---

### 🛡 Integração de Hardware e Estado Maior
Como DPI soberano, as raízes de assinatura (`Root CA`) e os *Master Keys* nunca são materializadas no disco ou na memória RAM comum. O NumoTrust é acoplado a um **HSM (Hardware Security Module)** de nível FIPS 140-2 Nível 3 / Nível 4. Toda a operação de assinatura da `Root CA` em um CRS submetido acontece no enclave de hardware.

### ✅ O Fluxo de Handshake Extremo (mTLS 1.3)
Quando uma Instituição envia um pagamento ao `NumoCore`:
1.  **Conexão Física:** O Load Balancer externo da rede privada recebe o pacote TCP vindo de um IP pre-aprovado via BGP/ASN (opcional).
2.  **Handshake:** O Gateway exige não apenas TLS, mas TSL Mútuo (mTLS 1.3).
3.  **Avaliação:** O cliente (IF) precisa enviar o seu certificado `client_cert`.
4.  **Assinatura Raiz:** O Gateway inspeciona o emissor. Este certificado foi emitido pela `Root CA` do NumoTrust? Se "Não", encerra conexão.
5.  **Validade (CRL):** Este certificado, mesmo que autêntico, está revogado no NumoTrust? Se "Sim", encerra a conexão.
6.  *Pass-through*: Somente com sucesso passará para a DMZ limpo e chegará à porta do *NumoCore*, permitindo a leitura da API de forma segura e soberana.
