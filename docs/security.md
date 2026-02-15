## Seguranca e identidade

### Objetivos
- Garantir autenticidade entre servicos.
- Reduzir superficie de ataque.
- Auditar operacoes criticas.

### mTLS
- CA central via **NumoTrust**.
- Certificados com SAN/CN alinhado ao `participant_id`.
- Validacao obrigatoria entre Core, Directory, Keys, Ledger e Admin-proxy.
- Rotacao coordenada e revogacao basica (CRL/OCSP ou lista interna).

### JWT / OpenID (opcional)
- Token para painel Admin e chamadas entre servicos.
- Escopos/roles definidos por modulo.

### Regras por modulo (resumo)
- **Trust**: autenticar `/issue` e `/rotate`, logs de auditoria, revogacao.
- **Keys**: rate limiting, validacao fina, CORS restrito, RBAC no Admin.
- **Directory**: tokens reais, permissoes por participante.
- **Ledger/Core**: idempotencia e auth forte.

### Checklist de seguranca
- Secrets fora do repo (.env local ou vault).
- Rotacao de chaves e certificados.
- Logs de auditoria para emissoes e operacoes sensiveis.
