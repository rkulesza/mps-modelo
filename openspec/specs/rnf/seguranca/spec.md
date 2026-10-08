# rnf/seguranca Specification

## Purpose
Requisitos não funcionais de controle de acesso, proteção de dados e auditoria.

## Requirements

### Requirement: NF-SEG-01 — Acesso apenas autenticado
O sistema NÃO DEVE expor nenhuma funcionalidade, exceto a tela de login, a usuários não autenticados.

**Prioridade:** Essencial

#### Scenario: Acesso direto por URL
- **GIVEN** um visitante sem sessão ativa
- **WHEN** ele acessa diretamente o endereço da grade de disponibilidade
- **THEN** o sistema redireciona para o login institucional

### Requirement: NF-SEG-02 — Trilha de auditoria
O sistema DEVE registrar quem aprovou, recusou ou cancelou cada reserva, com data e hora, e manter esse registro por pelo menos 2 anos.

**Prioridade:** Importante
**Casos de uso:** UC02, UC03

#### Scenario: Consulta de histórico
- **GIVEN** uma reserva foi aprovada e depois cancelada
- **WHEN** a Secretaria abre o histórico da reserva
- **THEN** o sistema exibe os dois eventos com autor, data e hora
