## Atividade

Implemente a seguinte diagrama: 

> **Nós**
>   - **Smartphone** — executa o App Mobile
>   - **Servidor de Aplicação** — executa:
>       - API REST
>       - PedidoService
>       - AuthService
>       - NotificaçãoService
> - **Servidor de Banco** — executa o Banco de Dados
> - **Serviços Externos** — disponibiliza:
>       - Gateway Pagamento
>       - Serviço de Mapas
> **Conexões**
> - Smartphone → Servidor de Aplicação — **HTTPS**
> - Servidor de Aplicação → Servidor de Banco — **TCP/SQL**
> - Servidor de Aplicação → Serviços Externos — **HTTPS**

- - - 

## Resposta:

### Codigo:
```puml
@startuml

node "Smartphone" as smartphone{
    artifact "App Mobile"
}

node "Servidor de Aplicação" as servidor{
    artifact "API REST" as api
    artifact "PedidoServer"
    artifact "AuthServer"
    artifact "NotificacaoServer"

}

database "Servidor BD" as bd{
    artifact "PostgreSQL DB"
}

cloud "Serviços Externos" as externos{
    artifact "GatewayPagamento"
    artifact "ServidorMapas"
}

smartphone --> servidor : HTTPS
servidor --> bd : TCP/SQL
servidor --> externos : HTTPS

@enduml
```

### Resultado

![Diagrama](diagrama.png)