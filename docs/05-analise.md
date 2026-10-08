# Análise de casos de uso — diagrama de classes de análise

> Seção 7 do modelo. Classes **sem atributos e métodos**, mas com os relacionamentos já definidos.
> Estereótipos ICONIX: «boundary» (fronteira), «control» (controle), «entity» (entidade).
> Os nomes das entidades vêm do [glossário](02-glossario.md).

```mermaid
classDiagram
    direction LR

    class TelaDisponibilidade { <<boundary>> }
    class FormularioReserva { <<boundary>> }
    class PainelSecretaria { <<boundary>> }
    class TelaLogin { <<boundary>> }
    class TelaUsuarios { <<boundary>> }

    class ControleConsulta { <<control>> }
    class ControleSolicitacao { <<control>> }
    class ControleAvaliacao { <<control>> }
    class ControleCancelamento { <<control>> }
    class ControleAutenticacao { <<control>> }
    class ControleUsuarios { <<control>> }

    class Usuario { <<entity>> }
    class Docente { <<entity>> }
    class Secretaria { <<entity>> }
    class Sala { <<entity>> }
    class Recurso { <<entity>> }
    class Reserva { <<entity>> }
    class ReservaRecorrente { <<entity>> }
    class RegistroAuditoria { <<entity>> }

    Usuario <|-- Docente
    Usuario <|-- Secretaria
    Sala "1" o-- "*" Recurso
    Docente "1" --> "*" Reserva : titular
    Reserva "*" --> "1" Sala
    ReservaRecorrente "1" *-- "2..*" Reserva
    Reserva "1" --> "*" RegistroAuditoria
    RegistroAuditoria "*" --> "1" Usuario : autor

    TelaDisponibilidade ..> ControleConsulta
    FormularioReserva ..> ControleSolicitacao
    PainelSecretaria ..> ControleAvaliacao
    TelaDisponibilidade ..> ControleCancelamento
    ControleConsulta ..> Sala
    ControleConsulta ..> Reserva
    ControleSolicitacao ..> Reserva
    ControleAvaliacao ..> Reserva
    ControleAvaliacao ..> RegistroAuditoria
    ControleCancelamento ..> Reserva
    ControleCancelamento ..> RegistroAuditoria
    TelaLogin ..> ControleAutenticacao
    TelaUsuarios ..> ControleUsuarios
    ControleAutenticacao ..> Usuario
    ControleUsuarios ..> Usuario
```

## Rastreabilidade caso de uso → classes de controle

| Caso de uso | Controle | Fronteiras |
|---|---|---|
| UC01 Solicitar reserva | ControleSolicitacao (usa ControleConsulta) | TelaDisponibilidade, FormularioReserva |
| UC02 Avaliar solicitação | ControleAvaliacao | PainelSecretaria |
| UC03 Cancelar reserva | ControleCancelamento | TelaDisponibilidade |
| UC05 Consultar disponibilidade | ControleConsulta | TelaDisponibilidade |
| UC06 Autenticar | ControleAutenticacao | TelaLogin |
| UC08 Cadastrar usuário | ControleUsuarios | TelaUsuarios |
| UC09 Listar usuários | ControleUsuarios | TelaUsuarios |
