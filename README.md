# Modelo de documentação de requisitos e projeto — MPS

Modelo de repositório para a disciplina **Métodos e Projeto de Software** (UFPB · Centro de Informática).
Ele substitui o antigo *Modelo de Documento de Requisitos* (.docx) por uma documentação **versionada em Git** e orientada a especificações (*spec-driven*), usando o [OpenSpec](https://github.com/Fission-AI/OpenSpec).

O repositório já vem preenchido com um **exemplo fictício**, o *ReservaCI* (reserva de salas do CI), para mostrar o nível de detalhe esperado. Substitua pelo seu sistema.

---

## 1. Como começar

1. Clique em **Use this template → Create a new repository** (um repositório por equipe).
2. Instale o OpenSpec (Node.js 20.19+):
   ```bash
   npm install -g @fission-ai/openspec@1
   ```
3. Troque o exemplo pelo seu sistema:
   - edite `openspec/config.yaml` (nome do sistema em `context`);
   - reescreva os arquivos de `docs/`;
   - apague as pastas de `openspec/specs/` e `openspec/changes/notificar-por-email/` e crie as suas.
4. Valide sempre antes de cada commit:
   ```bash
   openspec validate --all
   ```
   O aviso *"should contain SHALL or MUST"* é esperado: escrevemos em português, com **DEVE**.

Assistente de IA é **opcional**. Todos os arquivos são Markdown que você pode escrever à mão. Se a equipe quiser usar um, rode `openspec init --tools <ferramenta>` (por exemplo `github-copilot`, `claude` ou `cursor`). Isso adiciona os comandos `/opsx:propose`, `/opsx:apply` e `/opsx:archive` sem alterar o que já existe.

---

## 2. Onde está cada seção do modelo antigo

| Seção do modelo .docx | Neste repositório |
|---|---|
| Capa (nome do projeto e integrantes) | Este `README.md` (seção 7) |
| Histórico de revisões | Histórico do Git: commits, pull requests e `openspec/changes/archive/` |
| 1. Introdução (propósito, visão geral, documentos relacionados) | [`docs/01-visao.md`](docs/01-visao.md) §1 |
| 2. Descrição geral (motivação, problemas, visão, escopo negativo, usuários, restrições) | [`docs/01-visao.md`](docs/01-visao.md) §2 |
| 3. Glossário | [`docs/02-glossario.md`](docs/02-glossario.md) |
| 4. Elicitação de requisitos | [`docs/03-elicitacao.md`](docs/03-elicitacao.md) + `docs/03-elicitacao/anexos/` |
| 5.1 Requisitos funcionais | [`openspec/specs/<capacidade>/spec.md`](openspec/specs/) |
| 5.2 Requisitos não funcionais | [`openspec/specs/rnf/<categoria>/spec.md`](openspec/specs/rnf/) |
| 6. Especificação (3 casos de uso principais) | [`docs/04-casos-de-uso/`](docs/04-casos-de-uso/) |
| 6.1 Diagrama de casos de uso | [`docs/04-casos-de-uso/README.md`](docs/04-casos-de-uso/README.md) |
| 7. Diagrama de classes de análise | [`docs/05-analise.md`](docs/05-analise.md) |
| 8. Descrição da interface | [`docs/06-interface/`](docs/06-interface/) |
| 9. Diagramas de arquitetura | [`docs/07-arquitetura/`](docs/07-arquitetura/) + ADRs em `adr/` |

---

## 3. Estrutura

```text
.
├── README.md                     ← capa, mapa e regras
├── docs/
│   ├── 01-visao.md               ← introdução e descrição geral
│   ├── 02-glossario.md
│   ├── 03-elicitacao.md
│   ├── 04-casos-de-uso/          ← diagrama + UC01..UC03 detalhados
│   ├── 05-analise.md             ← classes de análise (ICONIX)
│   ├── 06-interface/             ← wireframes TL01..TLnn
│   ├── 07-arquitetura/           ← C4 + tabela RNF → decisão
│   │   └── adr/                  ← registros de decisão de arquitetura
│   └── _modelos/                 ← modelos em branco (requisito, caso de uso)
├── openspec/
│   ├── config.yaml               ← contexto e regras do projeto
│   ├── specs/                    ← REQUISITOS EM VIGOR (fonte da verdade)
│   │   ├── salas/spec.md
│   │   ├── reservas/spec.md
│   │   ├── autenticacao/spec.md
│   │   └── rnf/{usabilidade,desempenho,seguranca,confiabilidade}/spec.md
│   └── changes/                  ← mudanças propostas, ainda não incorporadas
│       ├── notificar-por-email/  ← exemplo: proposal, design, tasks, delta das specs
│       └── archive/              ← mudanças concluídas (histórico)
└── .github/
    ├── workflows/openspec.yml    ← valida as specs a cada push e PR
    └── pull_request_template.md
```

---

## 4. Convenções

**Identificadores**: são estáveis. Nunca renumere nem reaproveite um ID.

| Item | Formato | Exemplo |
|---|---|---|
| Requisito funcional | `RFnn` | RF03 |
| Requisito não funcional | `NF-CAT-nn` (numeração por categoria) | NF-DES-01 |
| Caso de uso | `UCnn` | UC01 |
| Tela | `TLnn` | TL02 |
| Decisão de arquitetura | `ADR-nnnn` | ADR-0002 |

**Requisito** (modelo completo em [`docs/_modelos/requisito.md`](docs/_modelos/requisito.md)):

```markdown
### Requirement: RF03 — Solicitar reserva
O sistema DEVE permitir que o Docente solicite ...

**Prioridade:** Essencial
**Casos de uso:** UC01

#### Scenario: Solicitação em horário livre
- **GIVEN** a sala está livre na quinta das 14h às 16h
- **WHEN** o Docente solicita esse horário
- **THEN** a solicitação é registrada com status "pendente"
```

- **Prioridade:** Essencial, Importante ou Desejável.
- Todo requisito tem **pelo menos um cenário**. Os cenários são os critérios de aceitação e viram testes depois.
- Num RNF, o `THEN` tem **número e unidade** (tempo, percentual, quantidade).
- Os cabeçalhos `Requirement`, `Scenario`, `GIVEN/WHEN/THEN`, `Purpose` e `Requirements` ficam **em inglês**, porque o OpenSpec os reconhece por esses nomes. O conteúdo é escrito em português.

**Diagramas**: são feitos em [Mermaid](https://mermaid.js.org/), que o GitHub desenha direto na página. PlantUML (`.puml`) é aceito quando a notação UML formal for necessária.

---

## 5. Fluxo de trabalho

### Entrega 1 — linha de base

Escreva diretamente em `docs/` e em `openspec/specs/`. Abra um pull request e marque o professor como revisor.

### Entregas seguintes — toda mudança de requisito é uma *change*

```bash
openspec new change <nome-da-mudanca>   # cria openspec/changes/<nome>/
```

1. **Proponha.** Preencha `proposal.md` (por quê, o que muda, o que fica fora do escopo), `specs/<capacidade>/spec.md` com o **delta** (`## ADDED`, `## MODIFIED` ou `## REMOVED Requirements`), `design.md` e `tasks.md`. Veja o exemplo em [`openspec/changes/notificar-por-email/`](openspec/changes/notificar-por-email/).
2. **Revise.** Abra um PR só com a proposta e discuta antes de implementar.
3. **Implemente.** Siga `tasks.md`, marcando `[x]` e fazendo um commit por tarefa ([Conventional Commits](https://www.conventionalcommits.org/pt-br/)).
4. **Arquive.** Ao concluir, o delta é aplicado em `openspec/specs/` e a change vai para `archive/`:
   ```bash
   openspec archive <nome-da-mudanca>
   ```

Num `MODIFIED`, copie o requisito **inteiro** e depois altere. O arquivamento substitui o bloco todo.

### Comandos úteis

| Comando | Para quê |
|---|---|
| `openspec list` / `openspec list --specs` | Listar changes abertas e capacidades |
| `openspec show <item>` | Ver uma spec ou change |
| `openspec validate --all` | Validar tudo (também roda no GitHub Actions) |
| `openspec status --change <nome>` | Ver quais artefatos da change faltam |
| `openspec view` | Painel interativo no terminal |

---

## 6. Checklist de entrega

- [ ] `openspec validate --all` sem erros (o selo do Actions está verde)
- [ ] Visão com escopo negativo e usuários descritos
- [ ] Glossário com os termos usados nas specs
- [ ] Elicitação com data, local, participantes e justificativa de cada técnica
- [ ] Todos os RF e RNF com ID, prioridade e cenários; RNFs mensuráveis
- [ ] Diagrama com todos os casos de uso + 3 casos de uso detalhados
- [ ] Diagrama de classes de análise com relacionamentos
- [ ] Wireframes das telas citadas nos casos de uso
- [ ] Arquitetura lógica e física + tabela mostrando como cada RNF é atendido
- [ ] Pelo menos um ADR

---

## 7. Equipe

**Sistema:** <nome do sistema>

| Integrante | Matrícula | GitHub |
|---|---|---|
| <nome> | <matrícula> | @<usuario> |
