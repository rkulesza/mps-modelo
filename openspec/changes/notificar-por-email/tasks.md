# Tasks

## 1. Documentação

- [ ] 1.1 Atualizar UC02 com o passo de justificativa (`docs/04-casos-de-uso/UC02-avaliar-solicitacao.md`)
- [ ] 1.2 Adicionar campo de justificativa no wireframe TL03 (`docs/06-interface/README.md`)
- [ ] 1.3 Escrever ADR-0003 — envio assíncrono de notificações

## 2. Implementação

- [ ] 2.1 Criar evento de domínio `StatusDaReservaAlterado`
- [ ] 2.2 Exigir justificativa na recusa (RF04) com teste do cenário "Recusa sem justificativa"
- [ ] 2.3 Criar tabela `notificacao_pendente` e job de envio
- [ ] 2.4 Implementar adaptador SMTP com teste usando servidor de e-mail falso

## 3. Verificação

- [ ] 3.1 Rodar `openspec validate notificar-por-email`
- [ ] 3.2 Demonstrar os cenários de RF08 em vídeo curto ou testes automatizados
