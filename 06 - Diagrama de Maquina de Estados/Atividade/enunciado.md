**Atividade — Diagrama de Máquina de Estados**

**1\. Saque Bancário**

Estados:

* Aguardando cartão;  
* Cartão inserido;  
* Aguardando senha;  
* Verificando senha;  
* Senha incorreta;  
* Aguardando valor;  
* Verificando saldo;  
* Saque autorizado;  
* Saque recusado;  
* Liberando dinheiro;  
* Devolvendo cartão;  
* Operação concluída;  
* Operação cancelada.

Situações:

1. O caixa eletrônico inicia **aguardando o cartão**.  
2. O cliente insere o cartão.  
3. O sistema solicita a senha.  
4. O cliente informa a senha e o sistema realiza a sua validação.  
5. A senha pode estar **correta ou incorreta**.  
6. Se a senha estiver correta, o sistema solicita o valor do saque.  
7. Se a senha estiver incorreta, o cliente poderá tentar novamente.  
8. Se o número máximo de tentativas de senha for excedido, a operação deverá ser cancelada.  
9. O cliente informa o valor que deseja sacar.  
10. O sistema verifica se existe saldo suficiente para realizar o saque.  
11. Se houver saldo suficiente, o saque é autorizado.  
12. Se não houver saldo suficiente, o saque é recusado.  
13. Após um saque recusado, o cliente poderá informar outro valor ou cancelar a operação.  
14. Quando o saque for autorizado, o caixa eletrônico libera o dinheiro.  
15. Após a retirada do dinheiro, o sistema devolve o cartão.  
16. Com o cartão devolvido, a operação é concluída.  
17. O cliente pode cancelar a operação durante as etapas em que o cancelamento é permitido.  
18. Em caso de cancelamento, o cartão deverá ser devolvido antes do encerramento da operação.

**2\. Locação de Carro**

Estados:

* Locação solicitada  
* Reserva confirmada  
* Reserva cancelada  
* Veículo retirado  
* Veículo em uso  
* Veículo devolvido  
* Em inspeção  
* Em manutenção  
* Locação encerrada

Situações:

1. O cliente solicita a locação de um carro.  
2. O sistema verifica a disponibilidade do veículo.  
3. Se houver veículo disponível, a reserva é confirmada.  
4. O cliente pode cancelar a reserva antes de retirar o veículo.  
5. O cliente retira o veículo na locadora.  
6. O veículo passa para o estado **Em uso**.  
7. O cliente devolve o veículo.  
8. Após a devolução, o veículo passa por uma inspeção.  
9. Se não houver problemas, a locação é encerrada.  
10. Se for identificado algum problema, o veículo deve passar por manutenção antes do encerramento da locação.  
11. Após a conclusão da manutenção, a locação também é encerrada.  
12. O diagrama deve possuir um **estado inicial** e um **estado final**.

**3\. Pedido de Comida**

Estados

* Pedido iniciado  
* Pedido realizado  
* Aguardando pagamento  
* Pagamento aprovado  
* Pagamento recusado  
* Pedido aceito pelo restaurante  
* Em preparação  
* Pronto  
* Aguardando entregador  
* Em entrega  
* Entregue  
* Cancelado

Situações:

1. O cliente inicia um pedido.  
2. O cliente confirma o pedido.  
3. O sistema passa a aguardar o pagamento.  
4. O pagamento pode ser **aprovado ou recusado**.  
5. Se o pagamento for recusado, o cliente poderá **tentar novamente ou cancelar** o pedido.  
6. Se o pagamento for aprovado, o pedido é encaminhado ao restaurante.  
7. O restaurante aceita o pedido.  
8. O restaurante inicia a preparação.  
9. Quando a preparação termina, o pedido fica pronto.  
10. O sistema aguarda um entregador.  
11. Quando um entregador aceita o pedido, ele realiza a retirada.  
12. O pedido entra em estado **Em entrega**.  
13. O entregador realiza a entrega.  
14. O pedido passa para o estado **Entregue**, encerrando o processo.  
15. O pedido poderá ser **cancelado** durante as etapas em que o cancelamento for permitido.

