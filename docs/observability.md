## Observabilidade

### Padrao minimo
- Logs estruturados (JSON) com `trace_id`.
- Metricas HTTP (latencia, status code, throughput).
- Tracing distribuido entre servicos.

### Itens recomendados
- Dashboards por servico (Core, Keys, Directory, Ledger).
- Alertas para latencia, erros 5xx e indisponibilidade.
- Healthchecks detalhados (dependencias + conexoes).

### Ferramentas sugeridas
- OpenTelemetry para tracing.
- Prometheus + Grafana para metricas.
- Loki/ELK para logs.
