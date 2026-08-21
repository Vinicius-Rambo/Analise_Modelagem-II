# Processo de realizar 

```platuml
@startuml
title Processo de Realizar Pedido

actor Cliente as cli
boundary "Tela de Pedidos" as tela
control "Pedido Controller" as controller
entity Pedido as ped
database "Banco de Dados" as bd
queue "Fila de Notificações" as fila

cli -> tela : Selecionar produtos

tela -> controller : Criar pedido
activate controller

controller -> ped : Criar()
activate ped

ped -> bd : Salvar Pedido
activate bd

bd --> ped : Confirmação
deactivate bd

ped --> controller : Pedido criado
deactivate ped

alt Pagamento aprovado
    controller ->> fila : Enviar evento
    controller --> tela : Pedido confirmado

else Pagamento recusado
    controller --> tela : Pedido confirmado
end

deactivate controller

tela --> cli : Exibir resultado
@enduml
```

### Imagem
![processo de realizar](imgs/processo.png)