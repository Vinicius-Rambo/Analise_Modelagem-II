# Atores

- Cliente 
- Atendente
- Entregador 
- Gateway de pagamento

# Casos de uso

#### Cliente: 
- UC01 - Fazer cadastro 
- UC02 - Consultar cardápio
- UC03 - Realizar pedido
- UC04 - Efetuar Pagamento
- UC05 - Acompanhar Status do pedido

#### Atendente:

- UC06 - Gerenciar Pedido  
- UC07 - Atualizar Status do pedido
- UC08 - Despachar Pedido

#### Entregador:

- UC09 - Aceitar rota de entrega
- UC10 - Confirmar entrega

### Casos de Uso Secundários (Ligados por Include/Extend)

- UC11 - Validar pagamento no Gateway
- UC12 - Fazer Login
- UC13 - Adicionar Observação
- UC14 - Aplicar Cupom de Desconto

# Relacionamentos Avançados

#### include (Obrigatório / Dependência)
- Efetuar Pagamento -> Validar pagamento no Gateway
Para que o cliente consiga pagar, o sistema obrigatoriamente precisa validar a transação com Gateway externo.

- Realizar Pedido -> Fazer Login 
O cliente não consegue fechar um pedido sem estar autenticado no sistema..

#### Extend (Opcional / variação)
- Adicionar Observação (Ex: Sem cebola) -> Realizar Pedido: 
O cliente pode fazer o pedido normalmente, mas adicionar uma observação é um passo opcional.

- Aplicar Cupom de Desconto -> Efetuar Pagamento:
Ao chegar na tela de pagamento, inserir um cupom é uma ação opciona

- Fazer cadastro -> Fazer login:
Se o usuário tentar entrar no sistema e perceber que não possui conta, ele tem a opção de realizar o cadastro a partir da tela de login.

# Diagrama

(![Diagrama](imgs/Pizzaria.png))