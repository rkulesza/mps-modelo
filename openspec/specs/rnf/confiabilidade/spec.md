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

### Requirement: NF-CON-03 — Falha de armazenamento tratada
O sistema NÃO DEVE encerrar nem perder os dados já gravados quando o armazenamento permanente falhar (arquivo inacessível, banco fora do ar); DEVE informar ao usuário que a operação não foi concluída.

**Prioridade:** Essencial
**Casos de uso:** UC08

#### Scenario: Arquivo de dados sem permissão de escrita
- **GIVEN** o sistema usa armazenamento em arquivo e o arquivo está sem permissão de escrita
- **WHEN** a Secretaria cadastra um usuário válido
- **THEN** o sistema informa "Não foi possível salvar o usuário" e continua em execução
