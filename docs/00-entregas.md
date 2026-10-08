# Cronograma de entregas — MPS 2026.2

> Este arquivo é do **professor**. Não altere; use-o como checklist.

## Princípio: especificar bem os 20% essenciais

Ninguém especifica o sistema inteiro antes de começar. A documentação cobre **em detalhe apenas o núcleo essencial**, cerca de 20% das funcionalidades: as que são implementadas nas sprints.

| Capacidade essencial | Sprint | Onde especificar |
|---|---|---|
| Gerenciamento de usuários (cadastro com validação, listagem, persistência) | S1, S2 | `openspec/specs/usuarios/` |
| CRUD de uma entidade principal do seu domínio, relacionada a Usuário ou a outra entidade | S3 | change `crud-<entidade>` |
| Relatórios de estatísticas de acesso dos usuários | S4 | change `relatorio-de-acessos` |
| Desfazer a última atualização da entidade principal | S5 | change `desfazer-atualizacao` |

As demais funcionalidades aparecem só na visão (`docs/01-visao.md` §2.3) e no diagrama de casos de uso. **Não** escreva requisitos detalhados para elas.

## Calendário

Cada data é uma **release**: PR de `develop` → `main` com a tag indicada (ver [CONTRIBUTING](../CONTRIBUTING.md)).

| Data | Entrega | Tag |
|---|---|---|
| **14/10/2026** | Entrega 1: documentação base + Sprints 1 e 2 | `v0.1.0` |
| **30/10/2026** | Entrega 2: documentação do essencial completa + Sprint 3 | `v0.2.0` |
| **11/11/2026** | Sprint 4: Padrões 2 | `v0.3.0` |
| **18/11/2026** | Sprint 5: Padrões 3 | `v0.4.0` |
| **09/12/2026** | Sprint 6: entrega final | `v1.0.0` |

---

## Entrega 1 — 14/10/2026 (Sprints 1 e 2)

### Documentação

- [ ] `README.md`: nome do sistema e equipe
- [ ] `docs/01-visao.md`: motivação, problemas, visão com escopo negativo, usuários, restrições
- [ ] `docs/02-glossario.md`
- [ ] `docs/03-elicitacao.md`: pelo menos 2 técnicas, com data, local e participantes
- [ ] `openspec/specs/usuarios/spec.md`: cadastrar usuário, regras de login, regras de senha, listar usuários
- [ ] RNFs ligados aos usuários: senha nunca exibida, persistência substituível, falha de armazenamento tratada
- [ ] **S1.1** Diagrama de casos de uso do **gerenciamento de usuários**, com pelo menos 2 tipos de usuário (`docs/04-casos-de-uso/`)
- [ ] **S1.2** Diagrama de classes de **análise** (fronteira, controle, entidade) do gerenciamento de usuários (`docs/05-analise.md`)
- [ ] **S2.1** Diagrama de classes de **projeto** com as exceções de validação e os 2 mecanismos de persistência (`docs/08-projeto.md`)
- [ ] ADR sobre a persistência substituível

### Código (siga o [CONTRIBUTING](../CONTRIBUTING.md))

- [ ] **S1** Divisão de pacotes/pastas (sugestão em `docs/08-projeto.md` §1)
- [ ] **S1** Adicionar usuário
- [ ] **S1** Armazenar os usuários numa coleção em memória (RAM)
- [ ] **S1** Listar todos os usuários
- [ ] **S2.2** Validação com exceções no cadastro de usuário:
  - Login: não vazio, no máximo 12 caracteres, sem números
  - Senha: [política padrão do AWS IAM](https://docs.aws.amazon.com/pt_br/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html), ou seja, de 8 a 128 caracteres, pelo menos 3 dos 4 tipos (maiúscula, minúscula, número, símbolo) e diferente do login
- [ ] **S2.3** Persistência também em arquivo binário **ou** banco de dados, escolhida no início da execução (RAM × permanente), tratando `IOException`/`SQLException`
- [ ] Um teste por cenário das regras de login e senha (nomes como `deve_recusar_login_com_numeros`)

---

## Entrega 2 — 30/10/2026 (Sprint 3: Padrões 1)

### Documentação

- [ ] Change `openspec/changes/crud-<entidade>/`: proposal, delta das specs (ADDED), design e tasks
- [ ] Diagrama de casos de uso completo (todos os casos de uso do sistema)
- [ ] **3 casos de uso detalhados**: 1 do gerenciamento de usuários + 2 da entidade principal
- [ ] `docs/06-interface/`: wireframes das telas dos 3 casos de uso
- [ ] `docs/07-arquitetura/`: arquitetura lógica e física + tabela "como cada RNF é atendido"
- [ ] **S3.1** Diagrama de classes de projeto atualizado com a nova entidade e a fachada
- [ ] ADR da fachada única

### Código

- [ ] **S3.2** CRUD da nova entidade, de preferência relacionada a Usuário ou a outra entidade
- [ ] **S3.2** `FacadeSingletonController`: fachada única (Facade + Singleton) para os controles, com um método que retorna a quantidade de entidades cadastradas
- [ ] **S3.3** Repositório atualizado; `openspec archive crud-<entidade>` ao concluir

---

## Sprint 4 — 11/11/2026 (Padrões 2)

### Documentação

- [ ] Change `relatorio-de-acessos`: requisitos dos relatórios de estatísticas de acesso (formatos, dados exibidos), com cenários
- [ ] ADRs: Repository + Factory; Adapter
- [ ] **S4.1** Diagrama de classes de projeto separando as camadas **business** e **infra** em todas as entidades
- [ ] **S4.5** Tabela de padrões em `docs/08-projeto.md` §3 preenchida com todos os padrões usados até aqui

### Código

- [ ] **S4.2** Repository para todas as entidades; Factory Method ou Abstract Factory para criar entidades ou escolher o tipo de repositório
- [ ] **S4.3** Adapter num cenário do projeto (sugestão: biblioteca de log)
- [ ] **S4.4** Template Method na camada business para gerar relatórios de acesso em mais de um formato (ex.: HTML e PDF)

---

## Sprint 5 — 18/11/2026 (Padrões 3)

### Documentação

- [ ] Change `desfazer-atualizacao`: requisito de desfazer a última atualização da entidade principal
- [ ] ADR: fachada baseada em Command
- [ ] **S5.3** Diagrama de classes de projeto e tabela de padrões atualizados

### Código

- [ ] **S5.1** Fachada da camada de negócio usando Command
- [ ] **S5.2** Memento para desfazer a última atualização da entidade principal

---

## Sprint 6 — 09/12/2026 (entrega final)

- [ ] Todas as changes arquivadas: `openspec list` vazio e `openspec/specs/` refletindo o sistema entregue
- [ ] Documentação consistente com o código: diagramas, casos de uso, ADRs
- [ ] Release `v1.0.0` em `main`
- [ ] *Demais itens: a definir pelo professor.*
