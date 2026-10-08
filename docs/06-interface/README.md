# Descrição da interface com o usuário

> Seção 8 do modelo. Rascunhos (wireframes) das telas que ajudam a entender os requisitos.
> Pode ser ASCII (como abaixo), foto de papel ou exportação do Figma/Excalidraw em `img/`.
> Cada tela tem um ID (TLnn) citado nos casos de uso.

## TL01 — Grade de disponibilidade

Relacionada a: UC01, UC03, UC05 · RF02, NF-USA-01, NF-USA-02

```text
┌──────────────────────────────────────────────────────────────┐
│ ReservaCI                       Minhas reservas │ Sair       │
├──────────────────────────────────────────────────────────────┤
│ Data [ 15/10/2026 ▾]  Horário [14:00]–[16:00]                │
│ Capacidade mín. [30]  Recursos [☑ projetor ☐ computadores]   │
│                                              [ Filtrar ]     │
├──────────────────────────────────────────────────────────────┤
│ Sala     Tipo         Cap.  Recursos           Ação          │
│ LAB-03   Laboratório   40   projetor, 40 PCs   [ Reservar ]  │
│ CI-105   Sala de aula  50   projetor           [ Reservar ]  │
└──────────────────────────────────────────────────────────────┘
```

## TL02 — Formulário de solicitação

Relacionada a: UC01 · RF03

```text
┌────────────────────────────────────────┐
│ Solicitar reserva                      │
│ Sala: LAB-03   Data: 15/10/2026        │
│ Horário: 14:00–16:00                   │
│ Finalidade: ( ) Aula (•) Prova         │
│             ( ) Defesa ( ) Evento      │
│ Observação: [______________________]   │
│ ☐ Repetir semanalmente até o fim       │
│   do período (UC07)                    │
│             [ Cancelar ] [ Confirmar ] │
└────────────────────────────────────────┘
```

## TL03 — Painel da Secretaria

Relacionada a: UC02 · RF04, NF-SEG-02

```text
┌──────────────────────────────────────────────────────────────┐
│ Solicitações pendentes (7)                                   │
├──────────────────────────────────────────────────────────────┤
│ 15/10 14–16  LAB-03  Prova   Prof. Carla   [Aprovar][Recusar]│
│ 16/10 08–10  CI-105  Aula    Prof. Diego   [Aprovar][Recusar]│
│ 17/10 terças 10–12 (recorrente, 9 datas)   [Aprovar][Recusar]│
└──────────────────────────────────────────────────────────────┘
```
