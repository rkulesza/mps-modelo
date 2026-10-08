# [UC01] Solicitar reserva

O Docente encontra uma sala livre e solicita sua reserva para uma data e faixa de horário.

| Campo | Valor |
|---|---|
| **Ator** | Docente |
| **Prioridade** | Essencial |
| **Requisitos** | RF02, RF03, NF-USA-01, NF-CON-01 |
| **Interfaces** | TL01, TL02 |

**Entradas e pré-condições**
- Docente autenticado (UC06).
- Data, faixa de horário, finalidade e, opcionalmente, capacidade mínima e recursos.

**Saídas e pós-condições**
- Sucesso: solicitação registrada com status *pendente*; horário bloqueado para outras solicitações.
- Falha: nenhuma reserva criada; o Docente vê os horários livres mais próximos.

## Fluxo principal

1. O Docente abre a grade de disponibilidade (TL01).
2. O Docente informa data, faixa de horário e filtros.
3. O sistema lista as salas livres (include UC05).
4. O Docente escolhe uma sala.
5. O sistema exibe o formulário de solicitação (TL02) já preenchido com sala, data e horário.
6. O Docente informa a finalidade e confirma.
7. O sistema verifica novamente a disponibilidade e registra a solicitação como *pendente*.
8. O sistema exibe o protocolo da solicitação.

## Fluxos secundários

**FA1 — Nenhuma sala livre (passo 3)**
1. O sistema informa que não há salas livres e sugere o horário livre mais próximo.
2. O Docente aceita a sugestão (volta ao passo 4) ou altera os filtros (volta ao passo 2).

**FE1 — Horário ocupado durante o preenchimento (passo 7)**
1. O sistema detecta que outro usuário reservou o horário.
2. O sistema informa o conflito e oferece os horários livres mais próximos. Volta ao passo 4.

**FE2 — Antecedência menor que 24 h (passo 6)**
1. O sistema recusa e orienta o Docente a contatar a Secretaria. O caso de uso termina.

> Os cenários de aceitação correspondentes estão em `openspec/specs/reservas/spec.md` (RF03).
