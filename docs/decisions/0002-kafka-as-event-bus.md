# 0002 - Kafka como barramento de eventos

## Status
Aceito

## Contexto
Os modulos precisam propagar eventos de negocio com alto throughput e
possibilidade de reprocessamento. E necessario suportar multiplos consumidores
com isolamento e escalabilidade.

## Decisao
Adotar Kafka como barramento de eventos principal para o Numo, com topicos
versionados e schema registry.

## Consequencias
- Padrao unico para eventos inter-servico.
- Necessidade de operar e monitorar cluster Kafka.
- Exige governanca de schemas e compatibilidade.

## Referencias
- `numo/docs/contracts.md`
- `numo/docs/modules/numoStream.md`
