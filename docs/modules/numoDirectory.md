## numoDirectory

### Responsabilidade
- Registro de participantes e permissoes.

### Estado atual (roadmap 0.1)
- CRUD basico.
- Token estatico.
- Sem mTLS/JWT integrado.

### APIs e contratos
- REST para participantes, permissoes e status.
- Eventos opcionais para onboarding/atualizacoes.

### Dependencias
- **Trust** para certificados.
- **Core/Keys** como consumidores do cadastro.

### Dados
- Persistencia de participantes e permissoes.

### Proximas evolucoes
- Autenticacao forte e tokens reais.
- Integracao direta com mTLS do Trust.
- Validacao de esquemas e observabilidade.
