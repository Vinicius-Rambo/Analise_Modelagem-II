# Atores
- Leitor
- Bibliotecário
- Sistema de Notificação

# Casos de uso
#### Leitor:

- UC01 - Consultar Acervo
- UC02 - Reservar Livro
- UC03 - Renovar Empréstimo
- UC04 - Pagar Multa

#### Bibliotecário:

- UC05 - Cadastrar Livro
- UC06 - Registrar Empréstimo
- UC07 - Registrar Devolução
- UC08 - Cadastrar Leitor

#### Sistema de Notificação:

- UC09 - Enviar Aviso de Vencimento

#### Casos de Uso Secundários (Ligados por Include/Extend)

- UC10 - Fazer Login
- UC11 - Verificar Pendências
- UC12 - Gerar Multa
- UC13 - Fazer Cadastro Online

# Relacionamentos Avançados

#### include (Obrigatório / Dependência)

- Reservar Livro -> Fazer Login
O leitor não consegue reservar um livro no sistema sem estar autenticado.

- Registrar Empréstimo -> Verificar Pendências
Para que o bibliotecário libere o livro, o sistema obrigatoriamente verifica se o leitor possui livros em atraso ou multas não pagas.

#### Extend (Opcional / variação)

- Gerar Multa -> Registrar Devolução:
O processo de devolução ocorre normalmente, mas a geração de uma multa é um passo opcional que só acontece se o livro estiver atrasado.

- Fazer Cadastro Online -> Fazer Login:
Se o usuário tentar entrar no sistema e perceber que não possui conta, ele tem a opção de realizar o cadastro a partir da tela de login.

# Diagrama

![Diagrama da bibliote](imgs/Biblioteca.png)