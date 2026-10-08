# reservas Specification

## Purpose
Ciclo de vida de uma reserva de sala: solicitação pelo docente, avaliação pela Secretaria, cancelamento e reservas recorrentes.

## Requirements

### Requirement: RF03 — Solicitar reserva
O sistema DEVE permitir que o Docente solicite a reserva de uma sala livre para uma data e faixa de horário, informando a finalidade (aula, prova, defesa, evento).

**Prioridade:** Essencial
**Casos de uso:** UC01

#### Scenario: Solicitação em horário livre
- **GIVEN** a sala "LAB-03" está livre na quinta das 14h às 16h
- **WHEN** o Docente solicita esse horário com finalidade "prova"
- **THEN** a solicitação é registrada com status "pendente" e o horário fica bloqueado para outras solicitações

#### Scenario: Horário ocupado no momento da confirmação
- **GIVEN** outro usuário reservou o mesmo horário enquanto o Docente preenchia o formulário
- **WHEN** o Docente confirma a solicitação
- **THEN** o sistema recusa a solicitação e oferece os horários livres mais próximos

#### Scenario: Antecedência mínima
- **GIVEN** faltam menos de 24 horas para o horário desejado
- **WHEN** o Docente tenta solicitar a reserva
- **THEN** o sistema recusa e orienta o Docente a contatar a Secretaria diretamente

### Requirement: RF04 — Avaliar solicitação
O sistema DEVE permitir que a Secretaria aprove ou recuse solicitações pendentes, exibindo-as em ordem de data de uso.

**Prioridade:** Importante
**Casos de uso:** UC02

#### Scenario: Aprovação
- **GIVEN** existe uma solicitação pendente
- **WHEN** a Secretaria aprova a solicitação
- **THEN** o status passa a "confirmada"

#### Scenario: Recusa
- **GIVEN** existe uma solicitação pendente
- **WHEN** a Secretaria recusa a solicitação
- **THEN** o status passa a "recusada" e o horário volta a ficar livre

### Requirement: RF05 — Cancelar reserva
O sistema DEVE permitir que o Docente cancele as próprias reservas pendentes ou confirmadas, liberando o horário imediatamente.

**Prioridade:** Importante
**Casos de uso:** UC03

#### Scenario: Cancelamento pelo titular
- **GIVEN** o Docente possui uma reserva confirmada para a próxima semana
- **WHEN** ele cancela a reserva
- **THEN** o status passa a "cancelada" e o horário aparece como livre na consulta

#### Scenario: Reserva de outro docente
- **GIVEN** a reserva pertence a outro Docente
- **WHEN** o Docente tenta cancelá-la
- **THEN** o sistema NÃO DEVE exibir a opção de cancelamento

### Requirement: RF06 — Reserva recorrente
O sistema DEVE permitir que o Docente solicite uma reserva semanal recorrente até o fim do período letivo, avaliada pela Secretaria como uma única solicitação.

**Prioridade:** Desejável
**Casos de uso:** UC07

#### Scenario: Recorrência sem conflitos
- **GIVEN** a sala está livre em todas as terças das 10h às 12h até o fim do período
- **WHEN** o Docente solicita a reserva recorrente
- **THEN** o sistema cria uma solicitação agrupando todas as ocorrências

#### Scenario: Recorrência com conflito parcial
- **GIVEN** duas das terças já estão ocupadas
- **WHEN** o Docente solicita a reserva recorrente
- **THEN** o sistema lista as datas em conflito e permite prosseguir apenas com as datas livres
