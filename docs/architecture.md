## Arquitetura

### Visao geral
O Numo e uma plataforma composta por servicos independentes que se comunicam
via HTTP e eventos. O repositorio central documenta como essas partes se
conectam, quais contratos existem e quais padroes devem ser seguidos.

### Componentes principais
- **Core**: orquestracao de operacoes e regras de negocio.
- **Directory**: registro de participantes e permissoes.
- **Keys**: gestao de chaves e validacoes.
- **Ledger**: registro de entradas, saldos e snapshots.
- **Stream**: barramento de eventos (Kafka).
- **Trust**: emissao e gestao de certificados.
- **Admin**: painel de operacao e proxy administrativo.

### Fluxo alto nivel (exemplo)
1. Participante criado no Directory.
2. Certificado emitido via Trust.
3. Chave registrada no Keys com validacao de identidade.
4. Operacoes passam pelo Core e geram eventos no Stream.
5. Ledger registra entradas e saldos com base nos eventos.

### Diagrama de contexto (alto nivel)
```mermaid
flowchart LR
    Admin[NumoAdmin] --> Core[NumoCore]
    Admin --> Directory[NumoDirectory]
    Admin --> Keys[NumoKeys]
    Admin --> Ledger[NumoLedger]
    Core --> Stream[NumoStream]
    Stream --> Ledger
    Directory --> Keys
    Trust[NumoTrust] --> Core
    Trust --> Directory
    Trust --> Keys
    Trust --> Ledger
```

### Diagrama de certificados (mTLS)
```mermaid
sequenceDiagram
    participant S as Servico (Core/Keys/Directory)
    participant T as NumoTrust
    S->>T: Solicita certificado (autenticado)
    T-->>S: Emite certificado
    S->>S: Armazena cert/key
    S->>S: Usa mTLS em chamadas inter-servico
```

### Fluxo end-to-end (cadastro -> emissao -> operacao)
```mermaid
sequenceDiagram
    participant A as Admin
    participant D as Directory
    participant T as Trust
    participant K as Keys
    participant C as Core
    participant S as Stream
    participant L as Ledger

    A->>D: Cadastra participante
    D-->>A: Participante criado
    A->>T: Emite certificado
    T-->>A: Certificado emitido
    A->>K: Registra chave
    K-->>A: Chave registrada
    A->>C: Inicia operacao
    C->>S: Publica evento
    S->>L: Consome evento
    L-->>C: Atualiza saldo
```

### Integracao entre servicos
- **mTLS** e/ou **JWT** para autenticacao entre servicos.
- **Schemas versionados** para eventos e APIs.
- **Observabilidade** padronizada (logs/metricas/traces).

### Decisoes arquiteturais
Documente aqui (ou em `docs/decisions/`) as principais escolhas tecnicas e
trade-offs. Ex: escolha de Kafka, Postgres, padrao de certificados, etc.
