## NumoCore: Motor de Retaguarda (RTGS)

O `NumoCore` é o cérebro da Infraestrutura Pública Digital (DPI). Ele não possui conta contábil ou registro de saldos (responsabilidade do `NumoLedger`), atuando estritamente como o orquestrador imutável de regras de negócio estatais e mensageria financeira padrão ISO 20022.

### 🎯 Responsabilidade
*   Receber intenções de liquidação de Instituições conectadas (via API Gateway).
*   Validar esquemas semânticos e gramaticais (ISO 20022 schemas: `pacs.008`, `camt.050`).
*   Verificar sanções, travas (compliance) contra o `NumoDirectory`.
*   Emitir comandos granulares, idempotentes e ordenados para o `NumoStream`.
*   Despachar Webhooks (`pacs.002` ou notificações `pacs.008`) para as instituições recebedoras.

---

### 🔌 API REST (Superfície de Conexão Externa)
O NumoCore expõe *endpoints* que, após a intercepção no API Gateway, processam requisições transacionais das Instituições Financeiras (IFs).

> **Aviso de Segurança (mTLS):** Toda chamada à API deve, obrigatoriamente, ser envelopada em uma sessão mTLS 1.3 utilizando o certificado SPIFFE emitido pelo `NumoTrust`. Requisições sem atestado criptográfico da IF são terminadas no handshake TCP pelo Gateway.

#### 1. Realizar Transferência de Crédito (`pacs.008`)
*   **Método:** `POST /v1/transfers`
*   **Headers:**
    *   `X-Idempotency-Key` (UUIDv4 - Obrigatório para evitar duplo processamento da mesma intent)
    *   `Content-Type: application/xml` (ou JSON conforme parsing estatal configurado)
*   **Payload Esperado (ISO 20022 Simplificado):**
    ```xml
    <Document>
      <FIToFICstmrCdtTrf>
        <GrpHdr>
          <MsgId>MSG123456</MsgId>
        </GrpHdr>
        <CdtTrfTxInf>
          <IntrBkSttlmAmt Ccy="BRL">1500.00</IntrBkSttlmAmt>
          <DbtrAgt><FinInstnId><BICFI>BANKABR1</BICFI></FinInstnId></DbtrAgt>
          <CdtrAgt><FinInstnId><BICFI>BANKBBR2</BICFI></FinInstnId></CdtrAgt>
        </CdtTrfTxInf>
      </FIToFICstmrCdtTrf>
    </Document>
    ```
*   **Respostas:**
    *   `202 Accepted`: Payload validado, evento enviado ao Kafka (`RESERVAR_SALDO`).
    *   `400 Bad Request`: Falha na semântica XSD do ISO 20022.
    *   `401 Unauthorized`: Falha de certificado mTLS.
    *   `422 Unprocessable Entity`: Regra de negócio violada (ex: Payer bloqueado no Directory).

#### 2. Consultar Status da Transação
*   **Método:** `GET /v1/transfers/{msgId}/status`
*   **Retorno:** Retorna o estado instantâneo extraído do materialized view do Core (ex: `PENDING_SETTLEMENT`, `SETTLED`, `REJECTED`).

---

### 🏗 Dependências Internas (gRPC/Kafka)
*   **Core ↔ Directory:** Consulta (gRPC) se o participante (BICFI) está ativo e autorizado a transacionar naquele escopo.
*   **Core ↔ Stream (Kafka):** Único ponto de mutação. O Core não escreve no banco. Ele envia protobufs mapeados ao tópico `numo.transactions.intent`.

### ✅ Padrões de Integração Exigidos (Instituições)
1. **Idempotência**: As Instituições devem manter e re-enviar exatamente o mesmo `X-Idempotency-Key` em retentativas (timeouts). O Core garante a captura via *hash table* (ex: Redis).
2. **Webhooks Assíncronos**: Instituições recebedoras devem expor URLs (configuradas no `NumoDirectory`) preparadas para receber POST requests da rede Root Node com a assinatura (HMAC ou JWS) do Banco Central.
