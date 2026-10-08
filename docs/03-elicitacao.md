# Elicitação de requisitos

> Seção 4 do modelo. Para cada técnica, registre **por que** foi escolhida e **quando, onde e com quem** foi aplicada.
> Anexos (roteiros, respostas, fotos) ficam em `docs/03-elicitacao/anexos/`.
> **Exemplo fictício.**

## 4.1 Entrevista semiestruturada com a Secretaria

| Campo | Registro |
|---|---|
| Data e horário | 10/03/2026, 10h–11h |
| Local | Secretaria do CI, sala 101 |
| Participantes | Ana (técnica, Secretaria), Bruno (técnico, Secretaria); equipe: Carla, Diego |
| Roteiro | `anexos/roteiro-entrevista-secretaria.md` |

**Por que esta técnica:** a Secretaria é o cliente e conhece as regras informais (antecedência, prioridades entre finalidades), que não estão escritas em nenhum documento.

**Principais achados:**
- Reservas pedidas com menos de 24 h são tratadas por telefone → RF03, cenário "Antecedência mínima".
- Recusas acontecem principalmente por manutenção de laboratório → RF04.
- No início do período, "metade da manhã" vai em responder e-mails de disponibilidade → P3, RF02.

## 4.2 Questionário com docentes

| Campo | Registro |
|---|---|
| Período de coleta | 12/03/2026 a 19/03/2026 |
| Meio | Formulário on-line enviado pela lista de docentes do CI |
| Participantes | 23 respostas de ~60 docentes |
| Instrumento e respostas | `anexos/questionario-docentes.csv` |

**Por que esta técnica:** os docentes são muitos e têm agenda difícil; o questionário permite quantificar problemas levantados na entrevista.

**Principais achados:**
- 19/23 perguntam à Secretaria antes de pedir uma sala → P2, RF02.
- 17/23 já descobriram uma recusa só ao chegar na sala → P4, change `notificar-por-email`.
- 11/23 usariam reserva semanal fixa → RF06 (Desejável).

## 4.3 Análise de documentos

| Campo | Registro |
|---|---|
| Data | 20/03/2026 |
| Documentos | Planilha "Reservas 2026.1"; Resolução de uso dos laboratórios |
| Responsável | Diego |

**Por que esta técnica:** a planilha mostra os dados reais (quantas reservas, quantos conflitos) e a resolução define regras obrigatórias.

**Principais achados:**
- 412 reservas e 14 conflitos em 2026.1 → P1, NF-CON-01.
- A resolução exige registro de quem autorizou o uso do laboratório → NF-SEG-02.

## 4.4 Considerações finais

As três técnicas se complementaram: a entrevista revelou regras, o questionário mediu a dor dos docentes e a análise de documentos deu números para priorizar. Faltou observar a Secretaria no pico de início de período (técnica de observação), o que fica para a próxima iteração.

### Rastreabilidade problema → requisito

| Problema | Requisitos |
|---|---|
| P1 | RF03, NF-CON-01 |
| P2 | RF02, NF-USA-01 |
| P3 | RF02, RF04 |
| P4 | RF08 (change `notificar-por-email`) |
