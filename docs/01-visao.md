# Visão do sistema — ReservaCI

> Equivale às seções 1 (Introdução) e 2 (Descrição geral) do modelo de documento de requisitos.
> **Exemplo fictício.** Substitua pelo conteúdo do seu sistema.

## 1. Introdução

### 1.1 Propósito deste repositório

Este repositório especifica o **ReservaCI**, sistema de reserva de salas e laboratórios do Centro de Informática. Ele é destinado à equipe de desenvolvimento, à Secretaria do CI (cliente) e ao professor da disciplina.

### 1.2 Organização

| Onde | O quê |
|---|---|
| `docs/01-visao.md` | Este arquivo: motivação, problemas, escopo, usuários, restrições |
| `docs/02-glossario.md` | Termos do domínio |
| `docs/03-elicitacao.md` | Técnicas de elicitação usadas e seus registros |
| `openspec/specs/` | **Requisitos funcionais e não funcionais** (fonte da verdade) |
| `docs/04-casos-de-uso/` | Diagrama de casos de uso e os 3 casos de uso detalhados |
| `docs/05-analise.md` | Diagrama de classes de análise |
| `docs/06-interface/` | Rascunhos de tela |
| `docs/07-arquitetura/` | Arquitetura (C4) e decisões (ADRs) |
| `docs/08-projeto.md` | Pacotes, diagrama de classes de projeto e padrões |
| `openspec/changes/` | Mudanças propostas nos requisitos, ainda não incorporadas |

### 1.3 Documentos relacionados

1. Resolução nº XX/20XX do CI — Normas de uso dos laboratórios; 20XX; Direção do CI; link.
2. Planilha "Reservas 2026.1" usada hoje pela Secretaria; mar/2026; Secretaria do CI.
3. [Glossário](02-glossario.md).

## 2. Descrição geral

### 2.1 Motivação

As reservas de salas e laboratórios são feitas hoje por e-mail e anotadas em uma planilha compartilhada. No início de cada período a Secretaria recebe centenas de pedidos em poucos dias, e conflitos só são descobertos quando duas turmas chegam à mesma sala.

### 2.2 Problemas identificados

| # | Problema | Quem é afetado | Evidência |
|---|---|---|---|
| P1 | Reservas sobrepostas para a mesma sala | Docentes, discentes | 14 conflitos registrados em 2026.1 (planilha) |
| P2 | Docente não sabe se a sala está livre antes de pedir | Docentes | Questionário: 19/23 consultam a Secretaria antes |
| P3 | Secretaria gasta horas respondendo e-mails de disponibilidade | Secretaria | Entrevista: "metade da manhã no início do período" |
| P4 | Docente não é avisado de recusa ou cancelamento | Docentes | Questionário: 17/23 |

### 2.3 Visão geral do sistema

**O sistema fará:**
- Cadastro de salas e laboratórios com capacidade e recursos.
- Consulta de disponibilidade por qualquer usuário autenticado.
- Solicitação, avaliação e cancelamento de reservas, inclusive recorrentes.
- Gerenciamento de usuários (Secretaria, Docente, Discente) com login e senha próprios.

**O sistema NÃO fará (escopo negativo):**

| Funcionalidade | Motivo |
|---|---|
| Alocação automática das turmas regulares do semestre | Já é feita no SIGAA; o ReservaCI importa apenas a ocupação resultante |
| Controle de chaves e acesso físico às salas | Fica com a portaria; avaliar em projeto futuro |
| Reserva de equipamentos avulsos (projetores, notebooks) | Fora do escopo do cliente nesta versão |

**Integração com outros sistemas:** o ReservaCI **não** é autocontido. Ele importa a ocupação das turmas regulares do SIGAA (planilha exportada, uma vez por período) e envia e-mails pelo servidor SMTP institucional.

### 2.4 Usuários do sistema

Todos os usuários têm vínculo com a UFPB e acessam o sistema principalmente pelo computador. Docentes também usam o celular para consultas rápidas.

| Usuário | Características | Principais dificuldades hoje |
|---|---|---|
| **Docente** | ~60 pessoas; uso esporádico, concentrado no início do período e em semanas de prova | Não sabe o que está livre; não é avisado de recusas |
| **Secretaria** | 2 técnicos administrativos; uso diário | Volume de e-mails; conferência manual de conflitos |
| **Discente** | Representantes de turma e organizadores de eventos; apenas consulta | Não tem acesso à planilha |

### 2.5 Suposições e restrições gerais

- **R1** — Deve rodar na infraestrutura de máquinas virtuais do CI (Linux, PostgreSQL disponível).
- **R2** — Senhas seguem a política padrão do AWS IAM (RF12) e nunca são exibidas (NF-SEG-03).
- **R3** — Dados pessoais limitados a nome, e-mail institucional e vínculo (LGPD).
- **S1** — Supõe-se que a exportação de turmas do SIGAA continuará disponível em formato planilha.
