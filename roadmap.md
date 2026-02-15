# Roadmap Numo – 0.1 → 1.0

## Estado atual (Release 0.1)
- **NumoCore**: API de pagamentos/contas básica, eventos via Kafka, sem auth forte, sem observabilidade estruturada.
- **NumoDirectory**: CRUD de participantes e permissões, token estático, sem mTLS/JWT integrado.
- **NumoKeys**: Registro/resolve/porta/delete com validações BR (EMAIL, PHONE, CPF/CNPJ, TAX_ID, RANDOM), mTLS opcional, persistência em memória/arquivo/Redis, health/metrics. mTLS pode validar CN vs participant_id e checar status no Directory.
- **NumoLedger**: Entradas, saldo, snapshots em Postgres; filtros básicos; sem auth/observabilidade.
- **NumoStream**: Kafka básico, sem schema registry.
- **NumoAdmin**: Painel TailAdmin (config/health/participants/keys/payments/ledger/audit/trust). Backend Node com proxy simples, audit file-based, auth básico/JWT opcional, CORS aberto.
- **NumoTrust**: CA self-signed, emissão simples, rotação manual, persistência de CA/cert/key em arquivo; sem revogação/CRL/OCSP; sem auth na emissão.
- **Infra/Scripts**: `restart-all.sh` para stacks principais; compose para cada serviço; sem CI/CD.

## Objetivos para 1.0

### Segurança & Identidade
- Padronizar mTLS entre serviços (Core, Directory, Keys, Ledger, Admin-proxy) usando CA do NumoTrust.
- NumoTrust: autenticação nas rotas `/issue`/`/rotate`, revogação básica (CRL/OCSP ou lista interna), rotação coordenada de CA, armazenamento seguro das chaves (secret store/HSM), logs de auditoria.
- NumoKeys: exigir mTLS + validação de CN/SAN vs participant_id; autorização fina; rate limiting; CORS restrito; RBAC no Admin.
- JWT/OpenID para Admin e chamadas inter-serviço (opcional).

### Persistência & Resiliência
- NumoKeys: storage robusto (Redis/DB) com cache, locks para portabilidade, TTL/expiração configuráveis, auditoria persistente.
- NumoLedger: hardening de schema, índices, idempotência forte, backups.
- NumoCore/Directory: validação de esquema, idempotência de operações sensíveis, replays seguros.
- NumoTrust: backup/restore seguro da CA, versionamento de chaves/certs.

### Observabilidade
- Métricas, logs estruturados e tracing distribuído em todos os serviços; health detalhado.
- Dashboards e alertas para serviços críticos (Core, Keys, Directory, Ledger).

### API & Contratos
- Schemas versionados para REST/eventos (OpenAPI/Avro/Protobuf); validação forte.
- NumoStream com schema registry e tópicos versionados; producers/consumers confiáveis.
- Admin: proxy seguro, gestão de certs (download/revogação), UX clara de estados e erros.

### Testes & Qualidade
- Suite de testes unit/integration para Core/Directory/Keys/Ledger/Trust.
- Testes de mTLS/JWT e fluxos fim a fim (registro de participante, emissão de cert, operação no Keys).
- CI/CD com lint, build, testes, scan de segurança e publicação de imagens.

### Serviços faltantes / Extensões
- NumoShield (antifraude), NumoRecover (devoluções), NumoEdge (gateway), NumoNode (SDK), NumoWatch (observabilidade), NumoOps (GitOps/infra) — especificar MVP ou mocks.

## Próximos passos sugeridos (ordem lógica)
1) Endurecer NumoTrust: autenticação nas rotas, persistência segura da CA, emissão com SAN correta e revogação básica.
2) Aplicar mTLS obrigatório entre serviços; configurar Directory real no Keys; tokens reais.
3) Persistência robusta e auditoria no Keys; rate limiting e CORS restrito.
4) Observabilidade unificada (metrics/logs/traces) + dashboards.
5) Schemas/contratos versionados (REST/eventos) e testes de integração/CI/CD.
