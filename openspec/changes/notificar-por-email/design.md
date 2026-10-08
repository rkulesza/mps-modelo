# Design: notificar-por-email

## Context

A avaliação de solicitações (UC02) acontece no painel da Secretaria. O servidor SMTP institucional às vezes demora vários segundos para responder, e a aprovação não pode ficar presa a isso (NF-DES-01, NF-CON-02).

## Goals / Non-Goals

**Goals:**
- Enviar o e-mail sem atrasar a resposta da aprovação/recusa.
- Não perder notificações se o SMTP estiver fora do ar.

**Non-Goals:**
- Garantir a entrega na caixa do destinatário (responsabilidade do servidor de e-mail).

## Decisions

- **Evento de domínio `StatusDaReservaAlterado`** publicado pelo caso de uso de avaliação; a camada de aplicação não conhece SMTP.
- **Fila persistida no banco (tabela `notificacao_pendente`)** processada por um job a cada minuto, em vez de envio síncrono. Alternativa descartada: broker de mensagens dedicado (RabbitMQ) — infraestrutura desproporcional ao volume (dezenas de e-mails/dia).
- Registrar a decisão como ADR-0003.

## Risks / Trade-offs

- Atraso de até ~1 minuto entre a avaliação e o e-mail → aceitável para o domínio.
- A tabela de pendências precisa de limpeza periódica.
