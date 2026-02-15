## Contratos e schemas

### APIs REST
- Versionar endpoints via `/v1`, `/v2` ou via header.
- Documentar com OpenAPI.
- Validacao forte de payloads (request/response).

### Exemplo OpenAPI (keys)
```yaml
openapi: 3.0.3
info:
  title: NumoKeys API
  version: 1.0.0
paths:
  /v1/keys:
    post:
      summary: Registra chave
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required: [participant_id, key_type, key_value]
              properties:
                participant_id: { type: string }
                key_type: { type: string, enum: [EMAIL, PHONE, CPF, CNPJ, TAX_ID, RANDOM] }
                key_value: { type: string }
      responses:
        "201":
          description: Chave registrada
```

### Exemplo OpenAPI (directory)
```yaml
openapi: 3.0.3
info:
  title: NumoDirectory API
  version: 1.0.0
paths:
  /v1/participants:
    post:
      summary: Cadastra participante
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required: [participant_id, name]
              properties:
                participant_id: { type: string }
                name: { type: string }
      responses:
        "201":
          description: Participante criado
```

### Eventos
- Definir schemas para eventos (Avro/Protobuf/JSON Schema).
- Versionar topicos e schemas.
- Garantir compatibilidade retroativa.

### Exemplo de evento (JSON Schema)
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "PaymentCreated",
  "type": "object",
  "required": ["payment_id", "participant_id", "amount", "currency", "created_at"],
  "properties": {
    "payment_id": { "type": "string" },
    "participant_id": { "type": "string" },
    "amount": { "type": "number" },
    "currency": { "type": "string" },
    "created_at": { "type": "string", "format": "date-time" }
  }
}
```

### Exemplo OpenAPI (ledger)
```yaml
openapi: 3.0.3
info:
  title: NumoLedger API
  version: 1.0.0
paths:
  /v1/ledger/entries:
    get:
      summary: Lista entradas
      parameters:
        - in: query
          name: participant_id
          schema: { type: string }
      responses:
        "200":
          description: Lista de entradas
```

### Exemplo OpenAPI (trust)
```yaml
openapi: 3.0.3
info:
  title: NumoTrust API
  version: 1.0.0
paths:
  /v1/certificates/issue:
    post:
      summary: Emite certificado
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              required: [subject, san]
              properties:
                subject: { type: string }
                san: { type: array, items: { type: string } }
      responses:
        "201":
          description: Certificado emitido
```

### Boas praticas
- Idempotencia para operacoes sensiveis.
- Trace_id propagado em chamadas e eventos.
- Erros padronizados com codigo e mensagem.

### Estrutura padrao de erros
```json
{
  "error": {
    "code": "NUMO_KEYS_VALIDATION",
    "message": "Chave invalida para o tipo informado",
    "details": {
      "field": "key_value"
    },
    "trace_id": "b0b1c5af-6b2d-4c7f-8d84-40b1a6a5f123"
  }
}
```

### Versionamento de APIs
- Endpoints versionados via `/v1`, `/v2`.
- Versoes antigas mantidas por tempo definido.
- Mudancas breaking exigem novo versionamento.

### Versionamento de eventos
- Topicos com sufixo de versao (ex: `payments.v1`).
- Schema registry com compatibilidade retroativa.
- Alteracoes incompatíveis exigem novo topico.
