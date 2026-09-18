# 1. Saque Bancário

```pulm
@startuml
title Saque Bancário

state "Aguardando cartão" as AguardandoCartao
state "Cartão inserido" as CartaoInserido
state "Aguardando senha" as AguardandoSenha
state "Verificando senha" as VerificandoSenha
state "Senha incorreta" as SenhaIncorreta
state "Aguardando valor" as AguardandoValor
state "Verificando saldo" as VerificandoSaldo
state "Saque autorizado" as SaqueAutorizado
state "Saque recusado" as SaqueRecusado
state "Liberando dinheiro" as LiberandoDinheiro
state "Devolvendo cartão" as DevolvendoCartao
state "Operação concluída" as OperacaoConcluida
state "Operação cancelada" as OperacaoCancelada

state EscolhaSenha <<choice>>
state EscolhaSaldo <<choice>>

[*] --> AguardandoCartao

AguardandoCartao --> CartaoInserido : Inserir cartão
CartaoInserido --> AguardandoSenha : Solicitar senha
AguardandoSenha --> VerificandoSenha : Informar senha
AguardandoSenha --> DevolvendoCartao : Cancelar

VerificandoSenha --> EscolhaSenha
EscolhaSenha --> AguardandoValor : [Senha correta]
EscolhaSenha --> SenhaIncorreta : [Senha incorreta]

SenhaIncorreta --> AguardandoSenha : Tentar novamente
SenhaIncorreta --> DevolvendoCartao : [Tentativas excedidas]

AguardandoValor --> VerificandoSaldo : Informar valor
AguardandoValor --> DevolvendoCartao : Cancelar

VerificandoSaldo --> EscolhaSaldo
EscolhaSaldo --> SaqueAutorizado : [Saldo suficiente]
EscolhaSaldo --> SaqueRecusado : [Saldo insuficiente]

SaqueRecusado --> AguardandoValor : Informar outro valor
SaqueRecusado --> DevolvendoCartao : Cancelar

SaqueAutorizado --> LiberandoDinheiro : Liberar dinheiro
LiberandoDinheiro --> DevolvendoCartao : Retirar dinheiro

DevolvendoCartao --> OperacaoConcluida : [Saque realizado]
DevolvendoCartao --> OperacaoCancelada : [Cancelado / Erro]

OperacaoConcluida --> [*]
OperacaoCancelada --> [*]
@enduml
```
![alt text](imgs/image.png)

# 2. Locação de Carro

```pulm
@startuml
title Locação de Carro

state "Locação solicitada" as LocacaoSolicitada
state "Reserva confirmada" as ReservaConfirmada
state "Reserva cancelada" as ReservaCancelada
state "Veículo retirado" as VeiculoRetirado
state "Veículo em uso" as VeiculoEmUso
state "Veículo devolvido" as VeiculoDevolvido
state "Em inspeção" as EmInspecao
state "Em manutenção" as EmManutencao
state "Locação encerrada" as LocacaoEncerrada

state VerificarDisponibilidade <<choice>>
state ResultadoInspecao <<choice>>

[*] --> LocacaoSolicitada

LocacaoSolicitada --> VerificarDisponibilidade : Verificar disponibilidade
VerificarDisponibilidade --> ReservaConfirmada : [Veículo disponível]
VerificarDisponibilidade --> LocacaoEncerrada : [Veículo indisponível]

ReservaConfirmada --> VeiculoRetirado : Retirar veículo
ReservaConfirmada --> ReservaCancelada : Cancelar reserva

ReservaCancelada --> LocacaoEncerrada : Encerrar

VeiculoRetirado --> VeiculoEmUso : Iniciar utilização
VeiculoEmUso --> VeiculoDevolvido : Devolver veículo
VeiculoDevolvido --> EmInspecao : Realizar inspeção

EmInspecao --> ResultadoInspecao
ResultadoInspecao --> LocacaoEncerrada : [Sem problemas]
ResultadoInspecao --> EmManutencao : [Problema identificado]

EmManutencao --> LocacaoEncerrada : Manutenção concluída
LocacaoEncerrada --> [*]
@enduml
```

![alt text](imgs/image2.png)

# 3. Pedido de Comida

```pulm
@startuml
title Pedido de Comida

state "Pedido iniciado" as PedidoIniciado
state "Pedido realizado" as PedidoRealizado
state "Aguardando pagamento" as AguardandoPagamento
state "Pagamento aprovado" as PagamentoAprovado
state "Pagamento recusado" as PagamentoRecusado
state "Pedido aceito pelo restaurante" as PedidoAceito
state "Em preparação" as EmPreparacao
state "Pronto" as Pronto
state "Aguardando entregador" as AguardandoEntregador
state "Em entrega" as EmEntrega
state "Entregue" as Entregue
state "Cancelado" as Cancelado

state EscolhaPagamento <<choice>>

[*] --> PedidoIniciado

PedidoIniciado --> PedidoRealizado : Confirmar pedido
PedidoRealizado --> AguardandoPagamento : Solicitar pagamento
PedidoRealizado --> Cancelado : Cancelar pedido

AguardandoPagamento --> EscolhaPagamento : Processar pagamento

EscolhaPagamento --> PagamentoAprovado : [Aprovado]
EscolhaPagamento --> PagamentoRecusado : [Recusado]

PagamentoRecusado --> AguardandoPagamento : Tentar novamente
PagamentoRecusado --> Cancelado : Cancelar pedido

PagamentoAprovado --> PedidoAceito : Restaurante aceita pedido
PedidoAceito --> EmPreparacao : Iniciar preparação

EmPreparacao --> Pronto : Finalizar preparação
Pronto --> AguardandoEntregador : Solicitar entregador

AguardandoEntregador --> EmEntrega : Entregador aceita e retira
AguardandoEntregador --> Cancelado : Cancelar pedido

EmEntrega --> Entregue : Realizar entrega
EmEntrega --> Cancelado : Cancelar pedido

Entregue --> [*]
Cancelado --> [*]
@enduml
```

![alt text](imgs/image3.png)