## numoStream

### Responsabilidade
- Barramento de eventos (Kafka).

### Estado atual (roadmap 0.1)
- Kafka basico.
- Sem schema registry.

### APIs e contratos
- Topicos versionados para eventos.
- Schema registry para compatibilidade.

### Dependencias
- **Core** como produtor principal.
- **Ledger** como consumidor principal.

### Dados
- Retencao de eventos conforme politica.

### Proximas evolucoes
- Schemas versionados.
- Producers/consumers confiaveis.
