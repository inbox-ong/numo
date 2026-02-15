## Testes e qualidade

### Tipos de testes
- Unitarios para regras locais de cada modulo.
- Integracao entre Core, Keys, Directory e Ledger.
- End-to-end para fluxos principais (cadastro -> emissao -> operacao).

### CI/CD
- Lint + formatadores obrigatorios.
- Build + testes em cada PR.
- Scan de seguranca e dependencias.

### Cobertura sugerida
- Core e Keys: 80%+.
- Fluxos criticos sempre cobertos por integracao.
