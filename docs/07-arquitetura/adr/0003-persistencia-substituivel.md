# ADR-0003: Tornar o mecanismo de persistência substituível

- **Status:** aceito
- **Data:** 2026-10-14
- **Requisitos relacionados:** NF-MAN-01, NF-CON-03

## Contexto

No início do projeto os usuários ficam só em memória (Sprint 1). Em seguida é preciso guardá-los também em arquivo binário ou banco de dados, escolhendo o mecanismo ao iniciar o sistema (Sprint 2), sem reescrever as regras de negócio.

## Decisão

As classes de negócio dependem de uma interface (`UsuarioRepository`) com operações de salvar e listar. Há uma implementação em memória e outra permanente (arquivo binário ou banco). A escolha é feita uma única vez, na inicialização, por parâmetro de configuração. Falhas de E/S são convertidas em uma exceção de negócio (`FalhaDeArmazenamentoException`).

## Alternativas consideradas

| Alternativa | Por que não |
|---|---|
| `if (modo == ARQUIVO)` espalhado pelos controles | Duplica decisões e mistura regra de negócio com detalhe de infraestrutura |
| Só banco de dados desde o início | Exige infraestrutura antes de haver regra de negócio para testar |

## Consequências

- Positivas: testes de negócio rodam em memória; trocar o mecanismo não altera os controles. Prepara o padrão Repository e a fábrica de repositórios da Sprint 4.
- Negativas: uma interface a mais para manter.
