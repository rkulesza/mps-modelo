# rnf/desempenho Specification

## Purpose
Requisitos não funcionais de tempo de resposta e capacidade de carga.

## Requirements

### Requirement: NF-DES-01 — Tempo de consulta
O sistema DEVE responder à consulta de disponibilidade em até 2 segundos no percentil 95 com até 200 usuários simultâneos.

**Prioridade:** Importante
**Casos de uso:** UC05

#### Scenario: Pico de início de período
- **GIVEN** 200 usuários simultâneos consultando a disponibilidade
- **WHEN** o teste de carga é executado por 10 minutos
- **THEN** 95% das respostas chegam em até 2 segundos
