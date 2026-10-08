# Proposta: notificar-por-email

## Why

Na elicitação (questionário com docentes, ver `docs/03-elicitacao.md`), 17 de 23 docentes disseram que só descobrem que a reserva foi recusada quando chegam à sala. Hoje o status só aparece se o docente abrir o sistema.

## What Changes

- Novo requisito **RF08 — Notificar mudança de status**: o docente recebe e-mail quando sua solicitação é aprovada, recusada ou cancelada pela Secretaria.
- **RF04 — Avaliar solicitação** passa a exigir justificativa na recusa, para que o e-mail explique o motivo.

**Fora do escopo:** notificações por WhatsApp/push, lembretes antes do horário da reserva, preferências de notificação por usuário.

## Capabilities

### New Capabilities
- (nenhuma)

### Modified Capabilities
- `reservas`: adiciona RF08 e modifica RF04 (justificativa obrigatória na recusa)

## Impact

- Novo adaptador de envio de e-mail na camada de infraestrutura (servidor SMTP institucional).
- Caso de uso UC02 ganha passo de justificativa; tela TL03 ganha campo de texto.
- Novo ADR sobre envio assíncrono de e-mail.
