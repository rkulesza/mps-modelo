# autenticacao Specification

## Purpose
Identificação dos usuários por meio da conta institucional, definindo o papel de cada um (Docente, Discente, Secretaria).

## Requirements

### Requirement: RF07 — Autenticar com conta institucional
O sistema DEVE autenticar usuários pelo provedor de identidade institucional e atribuir o papel conforme o vínculo (docente, discente ou técnico da Secretaria).

**Prioridade:** Essencial
**Casos de uso:** UC06

#### Scenario: Primeiro acesso de docente
- **GIVEN** o usuário possui vínculo ativo de docente
- **WHEN** ele se autentica pela primeira vez
- **THEN** o sistema cria seu perfil com papel "Docente"

#### Scenario: Vínculo inativo
- **GIVEN** o vínculo do usuário foi encerrado
- **WHEN** ele tenta se autenticar
- **THEN** o sistema nega o acesso e informa o motivo
