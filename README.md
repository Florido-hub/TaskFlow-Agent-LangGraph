# TaskFlow-Agent-LangGraph


## Fluxo de execução

``` mermaid
flowchart TD
    A([Início]) --> B[Receber mensagem do usuário]
    B --> C[Recuperar estado da sessão]
    C --> D[LLM: interpretar solicitação]

    D --> E{Precisa executar ferramenta?}

    E -->|Não| F[Gerar resposta textual]
    F --> Z[Atualizar estado e responder]

    E -->|Sim| G{Qual operação?}

    G -->|Consultar| H[Consultar tarefas]
    G -->|Criar| I[Validar dados da tarefa]
    G -->|Atualizar| J[Identificar tarefa e campos]
    G -->|Iniciar| K[Identificar tarefa]
    G -->|Concluir| L[Identificar tarefa]
    G -->|Excluir| M[Identificar tarefa]

    I --> N{Dados suficientes?}
    N -->|Não| O[Solicitar dados faltantes]
    O --> Z
    N -->|Sim| P[Executar ferramenta]

    J --> Q{Dados suficientes?}
    Q -->|Não| O
    Q -->|Sim| R[Executar atualização]

    K --> P
    L --> P
    H --> S[Retornar resultado da API]
    P --> S
    R --> S

    M --> T[Solicitar confirmação]
    T --> U{Usuário confirmou?}
    U -->|Não| V[Cancelar exclusão]
    U -->|Sim| W[Executar exclusão]
    W --> S
    V --> Z

    S --> X[LLM: interpretar resultado]
    X --> Z
    Z --> Y([Fim])
```
