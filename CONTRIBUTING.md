# Guia de Contribuição

Este documento define as práticas e convenções adotadas no projeto. Todo membro da equipe — humano ou agente IA — deve segui-las.

---

## 1. Estratégia de branches principais

O repositório possui duas branches de longa duração. Nenhuma delas recebe commits diretos.

```
main ──────────────────────────────────────────────► produção
  ▲                                          ▲
  │  merge (release ou hotfix)               │ hotfix
  │                                          │
develop ──────────────────────────────────► merge antes da release
  ▲         ▲          ▲
  │         │          │
feat/x   fix/y     refactor/z   ← branches de trabalho (curta duração)
```

### `main`

- Representa o estado **atual de produção**
- Todo commit em `main` é uma versão entregável e estável
- Só recebe merges vindos de `develop` (via release) ou de `hotfix/*`
- Cada merge em `main` deve ser **tagueado** com a versão: `v1.2.0`

### `develop`

- Branch de **integração contínua** — onde o trabalho da equipe converge
- Deve sempre estar em estado funcional (CI passando)
- Branches de feature, fix e refactor partem daqui e retornam aqui via PR
- Periodicamente promovida para `main` quando um conjunto de funcionalidades está pronto para release

### Fluxo resumido

```
1. Partir de develop
   git checkout develop && git pull
   git checkout -b feat/42-nome-da-feature

2. Desenvolver com commits atômicos

3. Abrir PR de feat/42-... → develop
   (revisão, CI, aprovação)

4. Merge em develop (squash ou merge commit — decisão do time)

5. Quando develop está pronta para ir a produção:
   PR develop → main  +  tag da versão
```

### Hotfix (bug crítico em produção)

```
main → hotfix/99-descricao → PR para main  +  PR para develop
```

Um hotfix parte de `main`, é corrigido, e depois é integrado em `develop` também — para não perder a correção na próxima release.

---

## 2. Commits

### Formato (Conventional Commits)

```
<tipo>(<escopo>): <descrição curta no imperativo>

[corpo opcional — o quê e por quê, não como]

[rodapé opcional: refs, breaking changes]
```

**Tipos permitidos:**

| Tipo       | Quando usar                                               |
|------------|-----------------------------------------------------------|
| `feat`     | Nova funcionalidade visível ao usuário/sistema            |
| `fix`      | Correção de bug                                           |
| `refactor` | Mudança interna sem alterar comportamento externo         |
| `test`     | Adição ou correção de testes                              |
| `docs`     | Apenas documentação                                       |
| `chore`    | Build, CI, dependências, configs — sem código de produção |
| `style`    | Formatação, espaçamento — sem mudança de lógica           |
| `perf`     | Melhoria de performance                                   |
| `revert`   | Reverte um commit anterior                                |

**Escopo:** camada ou módulo afetado (`domain`, `auth`, `api`, `ui`, `ci`, etc.).

**Exemplos válidos:**

```
feat(auth): adicionar autenticação via token JWT

fix(domain): corrigir cálculo de desconto para pedidos fracionados

refactor(user): extrair validação de e-mail para classe dedicada

docs(adr): registrar decisão de uso de event sourcing (ADR-004)
```

**Regras:**
- Descrição em **português**, no **imperativo** ("adicionar", não "adicionei" ou "adicionando")
- Máximo de **72 caracteres** na primeira linha
- Um commit = uma responsabilidade. Se precisar de "e" na descrição, considere dividir
- Commits de trabalho em progresso devem usar `wip:` e ser squashados antes do merge

---

## 3. Branches

```
<tipo>/<escopo-ou-issue>-<descricao-curta>
```

```
feat/42-autenticacao-jwt
fix/87-calculo-desconto-fracionado
refactor/user-validacao-email
docs/adr-event-sourcing
```

**Regras:**
- Nunca commitar diretamente em `main` ou `develop`
- Branches de feature e fix partem de `develop` (ver seção 1)
- Hotfixes partem de `main` e são integrados em `main` e `develop`
- Delete a branch após o merge

---

## 4. Práticas de Clean Code

> Independentes de linguagem. Válidas para qualquer camada.

### 4.1 Nomes revelam intenção

```
// ❌
int d;
bool flag;
void process(List x);

// ✅
int diasAteVencimento;
bool usuarioEstaAtivo;
void processarPedidosPendentes(List<Pedido> pedidos);
```

- Nomes de **variáveis e funções**: descrevem *o que são* ou *o que fazem*
- Nomes de **classes**: substantivos (`Pedido`, `AutenticadorDeUsuario`)
- Nomes de **funções/métodos**: verbos (`calcular`, `validar`, `buscar`)
- Evite abreviações que exijam contexto mental (`usrMgr` → `gerenciadorDeUsuario`)
- Evite prefixos redundantes (`pedido.pedidoId` → `pedido.id`)

### 4.2 Funções fazem uma coisa

- Uma função cabe em uma tela sem scroll → suspeite se precisar de mais
- Se você precisar usar "e" para descrever o que ela faz, extraia
- Parâmetros: idealmente 0–2; 3 é o limite; acima disso, agrupe em objeto

### 4.3 Não deixe comentários onde o código pode falar

```
// ❌ Comentário que repete o código
// Verifica se o usuário é maior de idade
if (usuario.idade >= 18) { ... }

// ✅ Nome que dispensa o comentário
if (usuario.eMaiorDeIdade()) { ... }
```

Comentários válidos: decisões de negócio não óbvias, workarounds com link para issue, advertências sobre efeitos colaterais.

### 4.4 Sem números mágicos ou strings soltas

```
// ❌
if (tentativas > 3) { ... }
status = "APROVADO";

// ✅
const val MAX_TENTATIVAS_LOGIN = 3;
if (tentativas > MAX_TENTATIVAS_LOGIN) { ... }
status = StatusPedido.APROVADO;
```

### 4.5 Regra do Escoteiro

> Deixe o código *ligeiramente* melhor do que você encontrou.

Não é refactoring massivo — é renomear uma variável confusa, extrair um bloco repetido, remover um TODO resolvido.

### 4.6 Testes são cidadãos de primeira classe

- Todo bug corrigido ganha um teste que o reproduz antes do fix
- Nomes de teste descrevem o cenário: `deve_retornar_erro_quando_email_invalido`
- Um teste = um comportamento verificado
- Testes não devem depender de ordem de execução

---

## 5. Pull Requests

**Título:** mesmo formato de commit (`feat(auth): adicionar login com Google`)

**Checklist antes de abrir o PR:**
- [ ] Testes passando localmente
- [ ] Cobertura não regrediu
- [ ] Nenhum `TODO` novo sem issue associada
- [ ] Documentação atualizada (se aplicável)
- [ ] ADR criado (se decisão arquitetural foi tomada)

**Tamanho:** PRs grandes são difíceis de revisar. Prefira PRs focados. Se ultrapassar ~400 linhas, justifique ou divida.

---

## 6. Para Agentes IA

Ao atuar neste repositório, siga adicionalmente:

1. **Leia `openspec/specs/` (e a change aberta em `openspec/changes/`) antes de implementar** — ali está o contrato do que deve ser feito
2. **Leia o ADR relevante** antes de propor mudanças arquiteturais
3. **Nunca altere contratos públicos** (interfaces, APIs, eventos) sem registrar um novo ADR
4. **Prefira edições cirúrgicas** a reescritas completas de arquivos existentes
5. **Documente suposições** no corpo do commit quando o requisito for ambíguo
6. **Não invente dependências** externas sem registrar no PR por que são necessárias
