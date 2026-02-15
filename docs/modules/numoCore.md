## numoCore

### Responsabilidade
- Orquestrar operacoes e regras de negocio.
- Gerar eventos para o Stream.

### Estado atual (roadmap 0.1)
- API de pagamentos/contas basica.
- Eventos via Kafka.
- Sem auth forte e observabilidade estruturada.

### APIs e contratos
- REST para pagamentos, contas e operacoes.
- Eventos publicados no Stream com versionamento.

### Dependencias
- **Directory** para validacao de participantes.
- **Keys** para validacao de chaves.
- **Stream** para publicacao de eventos.
- **Trust** para certificados.

### Dados
- Persistencia principal em banco relacional.
- Eventos como fonte de integracao.

### Proximas evolucoes
- mTLS/JWT obrigatorios.
- Idempotencia e validacao de esquema.
- Observabilidade completa.
