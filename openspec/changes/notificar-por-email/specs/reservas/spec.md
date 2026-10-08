# Spec Delta — reservas

## ADDED Requirements

### Requirement: RF08 — Notificar mudança de status
O sistema DEVE enviar e-mail ao Docente titular sempre que sua reserva for aprovada, recusada ou cancelada por outra pessoa, informando sala, data, horário, novo status e, na recusa, a justificativa.

**Prioridade:** Importante
**Casos de uso:** UC02

#### Scenario: Aprovação notificada
- **GIVEN** o Docente tem uma solicitação pendente
- **WHEN** a Secretaria aprova a solicitação
- **THEN** o Docente recebe um e-mail em até 5 minutos com o status "confirmada"

#### Scenario: Servidor de e-mail indisponível
- **GIVEN** o servidor de e-mail está fora do ar
- **WHEN** a Secretaria recusa uma solicitação
- **THEN** a recusa é registrada normalmente e o e-mail é enviado quando o servidor voltar

## MODIFIED Requirements

### Requirement: RF04 — Avaliar solicitação
O sistema DEVE permitir que a Secretaria aprove ou recuse solicitações pendentes, exibindo-as em ordem de data de uso. A recusa DEVE conter uma justificativa de no mínimo 10 caracteres.

**Prioridade:** Importante
**Casos de uso:** UC02

#### Scenario: Aprovação
- **GIVEN** existe uma solicitação pendente
- **WHEN** a Secretaria aprova a solicitação
- **THEN** o status passa a "confirmada"

#### Scenario: Recusa
- **GIVEN** existe uma solicitação pendente
- **WHEN** a Secretaria recusa a solicitação informando a justificativa "Sala reservada para manutenção"
- **THEN** o status passa a "recusada", a justificativa é registrada e o horário volta a ficar livre

#### Scenario: Recusa sem justificativa
- **GIVEN** existe uma solicitação pendente
- **WHEN** a Secretaria tenta recusar sem informar justificativa
- **THEN** o sistema impede a recusa e destaca o campo obrigatório
