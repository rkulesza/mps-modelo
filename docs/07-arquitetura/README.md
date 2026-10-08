# Arquitetura

> Seção 9 do modelo. Pelo menos um diagrama de arquitetura **lógica** e um de arquitetura **física**, e a explicação de **como cada requisito não funcional é atendido**.
> Diagramas no estilo [C4](https://c4model.com/). Decisões importantes ficam registradas como ADRs em [`adr/`](adr/).

## 9.1 Contexto (C4 nível 1)

```mermaid
flowchart TB
    docente["Docente<br/>[pessoa]"]
    secretaria["Secretaria<br/>[pessoa]"]
    discente["Discente<br/>[pessoa]"]
    sistema["ReservaCI<br/>[sistema]<br/>Reserva de salas e laboratórios"]
    idp["Provedor de identidade<br/>[sistema externo]"]
    smtp["Servidor de e-mail<br/>[sistema externo]"]
    sigaa["SIGAA<br/>[sistema externo]<br/>Exportação de turmas"]

    docente -->|consulta, solicita, cancela| sistema
    secretaria -->|cadastra salas, avalia| sistema
    discente -->|consulta| sistema
    sistema -->|autentica via OIDC| idp
    sistema -->|envia notificações| smtp
    sigaa -.->|planilha por período| sistema
```

## 9.2 Arquitetura lógica — contêineres e camadas (C4 nível 2)

Monolito modular em camadas (ver [ADR-0001](adr/0001-monolito-modular.md)). Dependências apontam sempre para dentro: interfaces → aplicação → domínio; infraestrutura implementa as portas definidas na aplicação.

```mermaid
flowchart TB
    subgraph web["Aplicação web (SPA) [contêiner]"]
        ui["Telas TL01–TL03"]
    end
    subgraph api["API ReservaCI [contêiner]"]
        direction TB
        interfaces["Interfaces<br/>controllers REST"]
        aplicacao["Aplicação<br/>casos de uso + portas"]
        dominio["Domínio<br/>Sala, Reserva, regras de conflito"]
        infra["Infraestrutura<br/>repositórios, gateway OIDC, SMTP"]
        interfaces --> aplicacao --> dominio
        infra -.->|implementa portas| aplicacao
    end
    db[("PostgreSQL [contêiner]")]

    ui -->|HTTPS/JSON| interfaces
    infra --> db
```

## 9.3 Arquitetura física — implantação

```mermaid
flowchart LR
    browser["Navegador<br/>(computador ou celular)"]
    subgraph vm["VM Linux — infraestrutura do CI"]
        nginx["nginx<br/>HTTPS + arquivos da SPA"]
        app["API ReservaCI<br/>(processo da aplicação)"]
        job["Job de notificações<br/>(a cada 1 min)"]
        pg[("PostgreSQL")]
    end
    idp["Provedor de identidade"]
    smtp["SMTP institucional"]

    browser -->|443| nginx --> app --> pg
    job --> pg
    job --> smtp
    app --> idp
```

## 9.4 Como cada requisito não funcional é atendido

| RNF | Decisão / tática arquitetural | Onde |
|---|---|---|
| NF-USA-01 | Formulário pré-preenchido a partir da grade; reserva em 3 interações | TL01 → TL02 |
| NF-USA-02 | SPA responsiva (layout em coluna abaixo de 600 px) | Contêiner web |
| NF-DES-01 | Índice por (sala, intervalo) no PostgreSQL; consulta de disponibilidade em uma única query | [ADR-0002](adr/0002-conflito-no-banco.md) |
| NF-SEG-01 | Todas as rotas da API exigem token OIDC; nginx só serve a SPA e o callback de login | Interfaces + gateway OIDC |
| NF-SEG-02 | Tabela de auditoria só de inserção, gravada na mesma transação da mudança de status | Infraestrutura |
| NF-CON-01 | Restrição de exclusão (`EXCLUDE USING gist`) impede sobreposição mesmo com requisições simultâneas | [ADR-0002](adr/0002-conflito-no-banco.md) |
| NF-CON-02 | Um único processo + banco na mesma VM; backup diário; monitoramento externo de disponibilidade | Implantação |
