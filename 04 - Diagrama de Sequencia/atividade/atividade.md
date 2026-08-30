## Realização de Pedido

Para o processo de realização de pedido, estruturei a comunicação entre o ator (Cliente) e os componentes do sistema. A Tela de Pedidos atua como interface, encaminhando a ação para o Pedido Controller, que orquestra a criação da entidade e a persistência no Banco de Dados. O diagrama utiliza um bloco alt para tratar a condição do pagamento (aprovado ou recusado) e representa a comunicação assíncrona com a Fila de Notificações utilizando uma seta apropriada.

### Codigo PlantUML

```plantuml
@startuml
skinparam maxMessageSize 150

actor Cliente
boundary "Tela de Pedidos" as Tela
control "Pedido Controller" as Controller
entity "Pedido" as Pedido
database "Banco de Dados" as BD
queue "Fila de Notificações" as Fila

Cliente -> Tela: selecionarProdutos()
Tela -> Controller: solicitarPedido(produtos)

Controller -> Pedido ** : criarPedido()
Controller -> BD: salvarPedido(Pedido)
BD --> Controller: confirmacaoRegistro()

alt Pagamento Aprovado
    Controller ->> Fila: notificarProcessamentoAsync()
    Controller --> Tela: pedidoConfirmado()
else Pagamento Recusado
    Controller --> Tela: erroProcessamento()
end

Tela --> Cliente: apresentarResultado()

@enduml
```

### Imagem:
![Pedido](pedido.png)

## Empréstimo de livro

Para o sistema de biblioteca estruturado em MVC, o Atendente interage com a InterfaceEmprestimo (View), que delega a lógica de negócio para o SistemaBiblioteca (Controller). O controlador realiza as verificações necessárias instanciando as classes de modelo (Usuario e Livro). Caso as regras de negócio sejam satisfeitas no bloco alt, a entidade Emprestimo é gerada, salva no BancoDeDados, o status do livro é alterado, e o sucesso é retornado à view. Caso contrário, o fluxo alternativo exibe a falha.

### Codigo PlantUML
```plantuml
@startuml
skinparam maxMessageSize 150

actor Atendente
boundary InterfaceEmprestimo as View
control SistemaBiblioteca as Controller
entity Usuario as ModelUsuario
entity Livro as ModelLivro
entity Emprestimo as ModelEmprestimo
database BancoDeDados as BD

Atendente -> View: solicitarEmprestimo(idUsuario, idLivro)
View -> Controller: processarSolicitacao(idUsuario, idLivro)

Controller -> ModelUsuario: verificarSituacao(idUsuario)
ModelUsuario --> Controller: statusUsuario

Controller -> ModelLivro: verificarDisponibilidade(idLivro)
ModelLivro --> Controller: statusLivro

alt Usuario Apto E Livro Disponivel
    Controller -> ModelEmprestimo ** : criarEmprestimo(idUsuario, idLivro)
    Controller -> BD: registrarEmprestimo(Emprestimo)
    BD --> Controller: confirmacaoSalvamento()
    
    Controller -> ModelLivro: atualizarStatus("emprestado")
    
    Controller --> View: confirmacaoEmprestimo()
    View --> Atendente: apresentarConfirmacao()
    
else Usuario Inapto OU Livro Indisponível
    Controller --> View: falhaEmprestimo(motivo)
    View --> Atendente: apresentarErro(motivo)
end

@enduml
```

### Imagem
![Imagme do emprestimo](emprestimo.png)

