## numoKeys

### Responsabilidade
- Registro, resolucao e remocao de chaves.
- Validacoes de identificadores BR (EMAIL, PHONE, CPF/CNPJ, TAX_ID, RANDOM).

### Estado atual (roadmap 0.1)
- mTLS opcional.
- Persistencia em memoria/arquivo/Redis.
- Health/metrics basicos.

### APIs e contratos
- REST para registro, resolucao e portabilidade.
- Validacoes BR de identificadores.

### Dependencias
- **Directory** para status de participante.
- **Trust** para certificados.
- **Core** para chamadas de negocio.

### Dados
- Storage de chaves e auditoria.

### Proximas evolucoes
- mTLS obrigatorio com validacao de CN/SAN.
- Autorizacao fina, rate limiting e CORS restrito.
- Auditoria persistente e storage robusto.
