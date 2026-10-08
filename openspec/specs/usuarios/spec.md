# usuarios Specification

## Purpose
Gerenciamento dos usuários do sistema (Secretaria, Docente e Discente): cadastro com validação de login e senha, listagem e autenticação.

## Requirements

### Requirement: RF07 — Cadastrar usuário
O sistema DEVE permitir que a Secretaria cadastre usuários informando nome, login, senha e papel (Secretaria, Docente ou Discente), recusando logins já existentes e informando ao usuário o motivo de qualquer recusa.

**Prioridade:** Essencial
**Casos de uso:** UC08

#### Scenario: Cadastro válido
- **GIVEN** não existe usuário com login "carla"
- **WHEN** a Secretaria cadastra login "carla", senha "Reserva#2026" e papel Docente
- **THEN** o usuário é armazenado e passa a aparecer na listagem

#### Scenario: Login já existente
- **GIVEN** já existe um usuário com login "carla"
- **WHEN** a Secretaria tenta cadastrar outro usuário com login "carla"
- **THEN** o sistema recusa o cadastro informando "Login já está em uso"

### Requirement: RF11 — Regras de login
O sistema DEVE aceitar apenas logins não vazios, com no máximo 12 caracteres e sem números.

**Prioridade:** Essencial
**Casos de uso:** UC08

#### Scenario: Login vazio
- **WHEN** a Secretaria tenta cadastrar um usuário com login vazio
- **THEN** o sistema recusa o cadastro informando "Login não pode ser vazio"

#### Scenario: Login com mais de 12 caracteres
- **WHEN** a Secretaria informa o login "carlamedeiros" (13 caracteres)
- **THEN** o sistema recusa o cadastro informando "Login deve ter no máximo 12 caracteres"

#### Scenario: Login com números
- **WHEN** a Secretaria informa o login "carla2"
- **THEN** o sistema recusa o cadastro informando "Login não pode conter números"

### Requirement: RF12 — Regras de senha
O sistema DEVE aceitar apenas senhas que sigam a política de senha padrão do AWS IAM: de 8 a 128 caracteres, com pelo menos 3 dos 4 tipos (maiúscula, minúscula, número, caractere não alfanumérico) e diferentes do login.

Caracteres não alfanuméricos aceitos: `! @ # $ % ^ & * ( ) _ + - = [ ] { } | '`

**Prioridade:** Essencial
**Casos de uso:** UC08

#### Scenario: Senha curta
- **WHEN** a Secretaria informa a senha "Ab#1" (4 caracteres)
- **THEN** o sistema recusa o cadastro informando "Senha deve ter entre 8 e 128 caracteres"

#### Scenario: Senha com poucos tipos de caractere
- **WHEN** a Secretaria informa a senha "reservasala" (só minúsculas)
- **THEN** o sistema recusa o cadastro informando "Senha deve combinar pelo menos 3 tipos: maiúsculas, minúsculas, números e símbolos"

#### Scenario: Senha com três tipos
- **WHEN** a Secretaria informa a senha "reserva#2026" (minúsculas, símbolo e números)
- **THEN** a senha é aceita

#### Scenario: Senha igual ao login
- **WHEN** a Secretaria informa login "Ana_Paula#" e senha "Ana_Paula#" (válida nas demais regras)
- **THEN** o sistema recusa o cadastro informando que a senha não pode ser igual ao login

### Requirement: RF09 — Listar usuários
O sistema DEVE permitir que a Secretaria liste todos os usuários cadastrados, exibindo nome, login e papel, sem exibir a senha.

**Prioridade:** Essencial
**Casos de uso:** UC09

#### Scenario: Listagem com usuários
- **GIVEN** existem 3 usuários cadastrados
- **WHEN** a Secretaria solicita a listagem
- **THEN** o sistema exibe os 3 usuários com nome, login e papel, sem a senha

#### Scenario: Nenhum usuário
- **GIVEN** não há usuários cadastrados além da própria Secretaria
- **WHEN** a Secretaria solicita a listagem
- **THEN** o sistema exibe apenas a Secretaria

### Requirement: RF10 — Autenticar com login e senha
O sistema DEVE autenticar usuários por login e senha e liberar apenas as funcionalidades do seu papel.

**Prioridade:** Essencial
**Casos de uso:** UC06

#### Scenario: Credenciais corretas
- **GIVEN** existe o usuário "carla" com papel Docente
- **WHEN** ela informa login e senha corretos
- **THEN** o sistema abre a grade de disponibilidade com as ações de Docente

#### Scenario: Credenciais incorretas
- **WHEN** o usuário informa uma senha incorreta
- **THEN** o sistema nega o acesso com a mensagem "Login ou senha inválidos", sem indicar qual dos dois está errado
