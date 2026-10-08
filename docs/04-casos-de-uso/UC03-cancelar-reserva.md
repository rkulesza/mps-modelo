# [UC03] Cancelar reserva

O Docente cancela uma reserva própria, liberando o horário para outros.

| Campo | Valor |
|---|---|
| **Ator** | Docente |
| **Prioridade** | Importante |
| **Requisitos** | RF05, NF-SEG-02 |
| **Interfaces** | TL01 |

**Entradas e pré-condições**
- Docente autenticado.
- Docente é titular de ao menos uma reserva *pendente* ou *confirmada* com data futura.

**Saídas e pós-condições**
- Reserva com status *cancelada*; horário livre na consulta.
- Evento registrado na trilha de auditoria.

## Fluxo principal

1. O Docente abre "Minhas reservas".
2. O sistema lista as reservas futuras do Docente.
3. O Docente seleciona uma reserva e escolhe "Cancelar".
4. O sistema pede confirmação.
5. O Docente confirma.
6. O sistema altera o status para *cancelada*, libera o horário e registra a auditoria.

## Fluxos secundários

**FA1 — Reserva recorrente (passo 3)**
1. O sistema pergunta se o cancelamento vale só para a data selecionada ou para todas as ocorrências futuras.
2. O Docente escolhe e o fluxo segue no passo 4.

**FA2 — Desistência (passo 5)**
1. O Docente não confirma; nada é alterado.
