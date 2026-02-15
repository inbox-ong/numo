## numoTrust

### Responsabilidade
- Autoridade certificadora (CA) do ecossistema.
- Emissao e rotacao de certificados.

### Estado atual (roadmap 0.1)
- CA self-signed.
- Rotacao manual.
- Sem revogacao/CRL/OCSP.
- Sem auth nas rotas de emissao.

### APIs e contratos
- REST para emissao, rotacao e revogacao.
- Politicas de certificacao por modulo.

### Dependencias
- **Directory** para validar participantes.
- **Admin** para operacao e auditoria.

### Dados
- Armazenamento seguro de CA/cert/key.

### Proximas evolucoes
- Autenticacao nas rotas `/issue` e `/rotate`.
- Revogacao basica e auditoria.
- Armazenamento seguro de chaves.
