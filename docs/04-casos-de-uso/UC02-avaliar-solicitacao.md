# [UC02] Avaliar solicitação

A Secretaria analisa as solicitações pendentes e aprova ou recusa cada uma.

| Campo | Valor |
|---|---|
| **Ator** | Secretaria |
| **Prioridade** | Importante |
| **Requisitos** | RF04, NF-SEG-02 |
| **Interfaces** | TL03 |

**Entradas e pré-condições**
- Usuário autenticado com papel Secretaria.
- Existe ao menos uma solicitação *pendente*.

**Saídas e pós-condições**
- Solicitação com status *confirmada* ou *recusada*.
- Evento registrado na trilha de auditoria (autor, data, hora).
- Em caso de recusa, horário liberado.

## Fluxo principal

1. A Secretaria abre o painel de solicitações (TL03).
2. O sistema lista as solicitações pendentes em ordem de data de uso.
3. A Secretaria seleciona uma solicitação e vê os detalhes (sala, data, horário, finalidade, docente).
4. A Secretaria aprova.
5. O sistema altera o status para *confirmada* e registra a auditoria.
6. O sistema retorna ao passo 2.

## Fluxos secundários

**FA1 — Recusar (passo 4)**
1. A Secretaria recusa a solicitação.
2. O sistema altera o status para *recusada*, libera o horário e registra a auditoria. Volta ao passo 2.

**FA2 — Solicitação recorrente (passo 3)**
1. O sistema mostra todas as ocorrências agrupadas; aprovar ou recusar vale para todas.
