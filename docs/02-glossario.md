# Glossário

> Seção 3 do modelo. Leia a referência indicada na disciplina sobre como escrever um glossário.
> Ordem alfabética. Use exatamente estes termos nas specs, casos de uso e no código (classes, tabelas).

| Termo | Definição | Sinônimos a evitar | Exemplo |
|---|---|---|---|
| **Disponibilidade** | Conjunto de intervalos em que uma sala ativa não tem reserva pendente nem confirmada. | vaga, horário aberto | "LAB-03 tem disponibilidade na quinta, 14h–16h" |
| **Docente** | Usuário com vínculo ativo de professor; pode solicitar e cancelar reservas. | professor, solicitante | — |
| **Finalidade** | Motivo declarado da reserva: aula, prova, defesa ou evento. | tipo de reserva | — |
| **Login** | Identificador único do usuário para entrar no sistema: até 12 caracteres, sem números (RF11). | usuário, username | carla |
| **Papel** | Conjunto de funcionalidades a que um usuário tem acesso: Secretaria, Docente ou Discente. | perfil, tipo de usuário | — |
| **Período letivo** | Intervalo entre o primeiro e o último dia de aula de um semestre, conforme o calendário acadêmico. | semestre | 2026.2 |
| **Reserva** | Ocupação de uma sala por um docente em uma data e faixa de horário. Possui um status. | agendamento, alocação | — |
| **Reserva recorrente** | Grupo de reservas semanais no mesmo dia e horário até o fim do período letivo, avaliado como uma única solicitação. | reserva fixa | — |
| **Sala** | Espaço físico reservável (sala de aula ou laboratório), identificado por um código único. | ambiente, espaço | LAB-03, CI-105 |
| **Secretaria** | Técnicos administrativos que cadastram salas e avaliam solicitações. | administrador | — |
| **Solicitação** | Reserva com status *pendente*, aguardando avaliação da Secretaria. | pedido | — |
| **Status da reserva** | Um dos valores: *pendente*, *confirmada*, *recusada*, *cancelada*. | situação | — |
| **Usuário** | Pessoa cadastrada no sistema com login, senha e um papel. | conta, pessoa | — |
