# rnf/manutenibilidade Specification

## Purpose
Requisitos não funcionais de facilidade de modificar e substituir partes do sistema, como o mecanismo de persistência.

## Requirements

### Requirement: NF-MAN-01 — Persistência substituível
O sistema DEVE permitir escolher, na inicialização, o mecanismo de armazenamento dos dados entre memória (RAM) e armazenamento permanente (arquivo binário ou banco de dados), sem alterar o código das regras de negócio.

**Prioridade:** Importante
**Casos de uso:** UC08, UC09

#### Scenario: Execução em memória
- **GIVEN** o sistema é iniciado com a opção de armazenamento "memoria"
- **WHEN** usuários são cadastrados e o sistema é reiniciado
- **THEN** a listagem fica vazia após o reinício

#### Scenario: Execução com armazenamento permanente
- **GIVEN** o sistema é iniciado com a opção de armazenamento "arquivo"
- **WHEN** usuários são cadastrados e o sistema é reiniciado
- **THEN** a listagem exibe os mesmos usuários de antes do reinício
