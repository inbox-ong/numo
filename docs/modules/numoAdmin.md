## numoAdmin

### Responsabilidade
- Painel administrativo e proxy.

### Estado atual (roadmap 0.1)
- TailAdmin com backend Node.
- Audit file-based.
- Auth basico/JWT opcional.
- CORS aberto.

### APIs e contratos
- Proxy administrativo para servicos internos.
- UI para configuracoes e auditoria.

### Dependencias
- **Core/Keys/Directory/Ledger/Trust** via proxy.
- **Auth** para RBAC.

### Dados
- Auditoria e configuracoes administrativas.

### Proximas evolucoes
- RBAC e CORS restrito.
- Proxy seguro e gestao de certs.
- Observabilidade e logs estruturados.
