# Implementação da Pizzaria Delivery:

Para "abençoar" o código e garantir que tudo funcione, começamos com o clássico:
```python
print("Olá Mundo!")
```

## 1. Criação da Classe `Sabor`
Esta classe é responsável por armazenar as informações de cada sabor disponível na pizzaria.

```python
class Sabor:
    def __init__(self, nome, ingredientes):
        self.nome = nome
        self.ingredientes = ingredientes

# Teste da classe Sabor
mussarela = Sabor("Mussarela", "queijo, molho, massa")
print(f"Sabor: {mussarela.nome} | Ingredientes: {mussarela.ingredientes}")
```

## 2. Criação da Classe `Pizza`
A classe `Pizza` recebe um tamanho e uma lista de sabores (objetos da classe `Sabor`). O método mágico `__str__` foi implementado para exibir a pizza de forma amigável no `print`.

```python
class Pizza:
    def __init__(self, tamanho):
        self.tamanho = tamanho
        self.sabores = []

    def adicionar_sabores(self, sabor):
        self.sabores.append(sabor)

    def __str__(self):
        nomes_sabores = [sabor.nome for sabor in self.sabores]
        lista_sabores = ", ".join(nomes_sabores)
        return f"Pizza {self.tamanho} | Sabores: {lista_sabores}"

# Teste da classe Pizza
calabresa = Sabor("Calabresa", "calabresa, mussarela, molho, cebola, massa")

pizza_mista = Pizza("G")
pizza_mista.adicionar_sabores(mussarela)
pizza_mista.adicionar_sabores(calabresa)
print(pizza_mista)
```

## 3. Criação da Classe `Usuario`
Representa o cliente que fará o pedido.

```python
class Usuario:
    def __init__(self, nome, telefone):
        self.nome = nome
        self.telefone = telefone

# Teste da classe Usuario
cliente = Usuario("Carlos", "(45) 99999-9999")
print(f"Cliente: {cliente.nome} | Tel: {cliente.telefone}")
```

## 4. Criação da Classe `Pedido`
A classe pedido junta tudo. Ela recebe um id, o objeto do cliente e armazena os itens (objetos da classe `Pizza`). 

*(Nota: Adicionados os métodos para inserir itens e imprimir o resumo do pedido).*

```python
class Pedido:
    def __init__(self, id_pedido, cliente):
        self.id_pedido = id_pedido
        self.cliente = cliente
        self.itens = []
        self.status = "Recebido"

    def adicionar_pizza(self, pizza):
        self.itens.append(pizza)
        
    def __str__(self):
        resumo = f"\n=== Pedido #{self.id_pedido} ===\n"
        resumo += f"Cliente: {self.cliente.nome}\n"
        resumo += f"Status: {self.status}\n"
        resumo += "Itens do Pedido:\n"
        for i, pizza in enumerate(self.itens, 1):
            resumo += f"  {i}. {pizza}\n"
        resumo += "==================="
        return resumo

# Teste Final Integrando Tudo
meu_pedido = Pedido(101, cliente)
meu_pedido.adicionar_pizza(pizza_mista)

print(meu_pedido)
```