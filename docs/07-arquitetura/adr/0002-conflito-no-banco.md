# ADR-0002: Garantir ausência de conflitos com restrição no banco

- **Status:** aceito
- **Data:** 2026-03-27
- **Requisitos relacionados:** NF-CON-01, NF-DES-01, RF03

## Contexto

Dois docentes podem confirmar a mesma sala e horário ao mesmo tempo (RF03, cenário "Horário ocupado no momento da confirmação"). Uma verificação "consulta e depois insere" na aplicação tem condição de corrida.

## Decisão

Usar uma restrição de exclusão do PostgreSQL sobre `(sala_id, intervalo)` para reservas com status *pendente* ou *confirmada*. A aplicação traduz a violação da restrição no aviso de conflito ao usuário.

## Alternativas consideradas

| Alternativa | Por que não |
|---|---|
| Lock pessimista na aplicação | Não funciona se houver mais de um processo; mais código de concorrência |
| Verificação só na aplicação | Condição de corrida; viola NF-CON-01 |

## Consequências

- Positivas: garantia mesmo sob concorrência; o mesmo índice acelera a consulta de disponibilidade (NF-DES-01).
- Negativas: dependência de recurso específico do PostgreSQL; testes de integração precisam de um PostgreSQL real.
