# 0004 - mTLS com CA propria (NumoTrust)

## Status
Aceito

## Contexto
Os servicos precisam de autenticacao forte, evitando credenciais estaticas e
garantindo identidade entre componentes internos.

## Decisao
Adotar mTLS entre servicos, com emissao de certificados pela CA do NumoTrust.
CN/SAN devem refletir o `participant_id` ou o servico.

## Consequencias
- Seguranca forte em todas as chamadas internas.
- Necessidade de governanca de certificados e revogacao.
- Impacto operacional na rotacao de chaves.

## Referencias
- `numo/docs/security.md`
- `numo/docs/modules/numoTrust.md`
