# ADR-0001: Usar monolito modular em camadas

- **Status:** aceito
- **Data:** 2026-03-25
- **Requisitos relacionados:** NF-CON-02, NF-DES-01, restrição R1

## Contexto

O sistema tem poucos usuários simultâneos (≤ 200), uma equipe de 4 estudantes e roda em uma única VM do CI (R1). Precisamos de regras de domínio testáveis sem banco nem rede.

## Decisão

Implementar um único processo de API organizado em camadas (domínio, aplicação, infraestrutura, interfaces), com módulos por capacidade (`salas`, `reservas`, `autenticacao`), alinhados às pastas de `openspec/specs/`.

## Alternativas consideradas

| Alternativa | Por que não |
|---|---|
| Microsserviços por capacidade | Custo operacional desproporcional; uma VM só; equipe pequena |
| Monolito sem camadas (MVC simples) | Regras de conflito ficariam acopladas ao framework e ao banco, difíceis de testar |

## Consequências

- Positivas: implantação simples; módulos rastreáveis até as specs; domínio testável isoladamente.
- Negativas: escala apenas verticalmente — aceitável para o volume previsto.
