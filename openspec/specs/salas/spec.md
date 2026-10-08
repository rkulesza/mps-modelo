# salas Specification

## Purpose
Cadastro das salas e laboratórios do Centro de Informática e consulta da sua disponibilidade por qualquer usuário autenticado.

## Requirements

### Requirement: RF01 — Cadastrar sala
O sistema DEVE permitir que a Secretaria cadastre, edite e desative salas, informando código, tipo (sala de aula ou laboratório), capacidade e recursos disponíveis (projetor, computadores).

**Prioridade:** Essencial
**Casos de uso:** UC04

#### Scenario: Cadastro com dados válidos
- **GIVEN** a Secretaria está autenticada
- **WHEN** ela informa código "LAB-03", tipo laboratório, capacidade 40 e confirma
- **THEN** a sala passa a aparecer na consulta de disponibilidade

#### Scenario: Código duplicado
- **GIVEN** já existe uma sala com código "LAB-03"
- **WHEN** a Secretaria tenta cadastrar outra sala com o mesmo código
- **THEN** o sistema recusa o cadastro e informa que o código já está em uso

#### Scenario: Desativar sala com reservas futuras
- **GIVEN** a sala "LAB-03" possui reservas confirmadas para as próximas semanas
- **WHEN** a Secretaria desativa a sala
- **THEN** o sistema exige confirmação e notifica os docentes cujas reservas serão canceladas

### Requirement: RF02 — Consultar disponibilidade
O sistema DEVE exibir a grade semanal de ocupação de uma sala e permitir filtrar salas livres por data, faixa de horário, capacidade mínima e recursos.

**Prioridade:** Essencial
**Casos de uso:** UC01, UC05

#### Scenario: Filtrar salas livres
- **GIVEN** existem 12 salas ativas, 5 delas ocupadas na terça das 08h às 10h
- **WHEN** o usuário filtra por terça, 08h–10h, capacidade mínima 30
- **THEN** o sistema lista apenas as salas livres nesse intervalo com capacidade maior ou igual a 30

#### Scenario: Nenhuma sala disponível
- **GIVEN** todas as salas que atendem ao filtro estão ocupadas
- **WHEN** o usuário aplica o filtro
- **THEN** o sistema informa que não há salas livres e sugere o horário livre mais próximo
