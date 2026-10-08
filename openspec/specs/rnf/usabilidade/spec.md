# rnf/usabilidade Specification

## Purpose
Requisitos não funcionais de facilidade de uso da interface, material de ajuda e acessibilidade.

## Requirements

### Requirement: NF-USA-01 — Reserva em poucos passos
O sistema DEVE permitir concluir uma solicitação de reserva a partir da tela inicial em no máximo 3 interações principais (filtrar, escolher horário, confirmar).

**Prioridade:** Importante
**Casos de uso:** UC01

#### Scenario: Teste com usuário novo
- **GIVEN** um docente que nunca usou o sistema
- **WHEN** ele recebe a tarefa "reserve um laboratório para quinta à tarde"
- **THEN** ele conclui a tarefa sem ajuda em até 2 minutos

### Requirement: NF-USA-02 — Uso em celular
O sistema DEVE ser utilizável em telas a partir de 360 px de largura sem rolagem horizontal.

**Prioridade:** Desejável

#### Scenario: Consulta pelo celular
- **GIVEN** um usuário acessa o sistema em um celular com tela de 360 px
- **WHEN** ele abre a grade de disponibilidade
- **THEN** a grade é exibida sem rolagem horizontal
