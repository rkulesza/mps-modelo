# rnf/confiabilidade Specification

## Purpose
Requisitos não funcionais de integridade dos dados e disponibilidade do serviço.

## Requirements

### Requirement: NF-CON-01 — Sem reservas sobrepostas
O sistema NÃO DEVE permitir duas reservas pendentes ou confirmadas para a mesma sala com horários sobrepostos, mesmo sob solicitações simultâneas.

**Prioridade:** Essencial
**Casos de uso:** UC01, UC07

#### Scenario: Solicitações concorrentes
- **GIVEN** dois docentes solicitam a mesma sala e horário no mesmo instante
- **WHEN** as duas requisições chegam ao servidor
- **THEN** exatamente uma é registrada e a outra recebe aviso de conflito

### Requirement: NF-CON-02 — Disponibilidade em horário letivo
O sistema DEVE estar disponível 99% do tempo entre 07h e 22h nos dias letivos.

**Prioridade:** Importante

#### Scenario: Medição mensal
- **GIVEN** o monitoramento registra a disponibilidade a cada minuto
- **WHEN** o relatório mensal é gerado
- **THEN** a disponibilidade no horário letivo é de pelo menos 99%
