### **Implementação de Diagramas de Sequência**

1. ### **Caso de uso: Realização de Pedido**

Considere um sistema de vendas on-line no qual um **Cliente** seleciona produtos e realiza um pedido.

O sistema possui uma organização com os seguintes participantes:

* **Ator:** `Cliente`;  
* **Interface:** `Tela de Pedidos`;  
* **Controlador:** `Pedido Controller`;  
* **Entidade:** `Pedido`;  
* **Persistência:** `Banco de Dados`;  
* **Comunicação assíncrona:** `Fila de Notificações`.

### **Atividade**

Modele, utilizando um **Diagrama de Sequência UML**, o processo de realização de um pedido.

Considere o seguinte cenário:

1. O cliente seleciona os produtos que deseja comprar.  
2. A **Tela de Pedidos** envia a solicitação para o **Pedido Controller**.  
3. O controlador cria um novo pedido.  
4. O pedido é salvo no **Banco de Dados**.  
5. O sistema recebe a confirmação de que o pedido foi registrado.  
6. Após a criação do pedido, ocorre a verificação do pagamento.

Considere dois possíveis resultados:

* **Pagamento aprovado:** o sistema envia um evento de forma assíncrona para a **Fila de Notificações** e informa à tela que o pedido foi confirmado.  
* **Pagamento recusado:** o sistema informa à tela que ocorreu um erro no processamento do pedido.

Por fim, a **Tela de Pedidos** apresenta o resultado da operação ao cliente.

### **2\. Caso de uso: Empréstimo de livro**

Considere um sistema de biblioteca no qual um **Atendente** realiza o processo de empréstimo de um livro.

O sistema utiliza uma organização baseada no padrão **MVC (Model–View–Controller)**, composta pelos seguintes elementos:

* **Ator:** `Atendente`;  
* **View:** `InterfaceEmprestimo`;  
* **Controller:** `SistemaBiblioteca`;  
* **Model:** `Usuario`, `Livro` e `Emprestimo`;  
* **Persistência:** `BancoDeDados`.

### **Atividade**

Modele, utilizando um **Diagrama de Sequência UML**, o cenário de realização de um empréstimo de livro.

Considere o seguinte fluxo principal:

1. O atendente solicita o empréstimo de um livro para um usuário.  
2. A interface envia a solicitação ao sistema.  
3. O sistema verifica a situação do usuário.  
4. O sistema verifica a disponibilidade do livro.  
5. Caso o usuário esteja apto e o livro esteja disponível, o sistema cria o empréstimo.  
6. O empréstimo é registrado no banco de dados.  
7. O status do livro é atualizado para **emprestado**.  
8. A interface apresenta a confirmação do empréstimo ao atendente.

Considere também um fluxo alternativo para os casos em que:

* o usuário não está apto para realizar o empréstimo; ou  
* o livro não está disponível.

