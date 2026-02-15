# 0003 - Postgres para ledger e snapshots

## Status
Aceito

## Contexto
O Ledger precisa de consistencia transacional e consultas agregadas
eficientes, com historico confiavel e mecanismos de backup.

## Decisao
Usar Postgres como banco principal do NumoLedger para entradas, saldos e
snapshots.

## Consequencias
- Forte consistencia e suporte a indices.
- Requer estrategia de backup e tuning.
- Dependencia de operacao do banco.

## Referencias
- `numo/docs/modules/numoLedger.md`
