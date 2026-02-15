## numoLedger

### Responsabilidade
- Registro de entradas e saldos.
- Snapshots em Postgres.

### Estado atual (roadmap 0.1)
- Filtros basicos.
- Sem auth/observabilidade.

### APIs e contratos
- REST para consultas de saldo e entradas.
- Consumo de eventos do Stream.

### Dependencias
- **Stream** para eventos.
- **Core** para operacoes principais.
- **Trust** para certificados.

### Dados
- Postgres para entradas e snapshots.

### Proximas evolucoes
- Idempotencia forte e indices.
- Backups e hardening de schema.
- Observabilidade completa.
