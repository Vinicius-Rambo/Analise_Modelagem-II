### Biblioteca

Para a biblioteca, Leitor e Bibliotecario também herdam de um usuário base. Criei a distinção entre Livro (o catálogo geral) e Exemplar (a cópia física que é efetivamente emprestada). O Sistema de Notificação também virou uma interface.

### Codigo PlantUML

```plantuml
@startuml
skinparam classAttributeIconSize 0

' --- Interfaces Externas ---
interface ISistemaNotificacao {
    + enviarAvisoVencimento(leitor: Leitor, emprestimo: Emprestimo): void
}

' --- Classes Base e Atores ---
abstract class Usuario {
    - id: Int
    - nome: String
    - email: String
    - senha: String
    + fazerLogin(): Boolean
}

class Leitor {
    - matricula: String
    - statusRegular: Boolean
    + fazerCadastroOnline(): void
    + consultarAcervo(): List<Livro>
    + reservarLivro(livro: Livro): Reserva
    + renovarEmprestimo(emprestimoId): Boolean
    + pagarMulta(multaId): void
}

class Bibliotecario {
    - crb: String
    + cadastrarLeitor(dados): Leitor
    + cadastrarLivro(dados): Livro
    + registrarEmprestimo(leitor, exemplar): Emprestimo
    + registrarDevolucao(emprestimo): void
    + verificarPendencias(leitor): Boolean
    + gerarMulta(emprestimo): Multa
}

Usuario <|-- Leitor
Usuario <|-- Bibliotecario

' --- Entidades de Negócio ---
class Livro {
    - isbn: String
    - titulo: String
    - autor: String
    - editora: String
    - anoPublicacao: Int
}

class Exemplar {
    - codigoBarras: String
    - disponivel: Boolean
}

class Emprestimo {
    - id: Int
    - dataEmprestimo: Date
    - dataDevolucaoPrevista: Date
    - dataDevolucaoReal: Date
    - status: String
    + calcularAtraso(): Int
}

class Reserva {
    - id: Int
    - dataReserva: Date
    - status: String
}

class Multa {
    - id: Int
    - valor: Float
    - dataGeracao: Date
    - statusPagamento: String
}

' --- Relacionamentos ---
Livro "1" *-- "1..*" Exemplar : possui >

Leitor "1" -- "0..*" Emprestimo : realiza >
Leitor "1" -- "0..*" Reserva : faz >
Reserva "0..*" -- "1" Livro : referente a >

Emprestimo "1" -- "1..*" Exemplar : contem >
Emprestimo "1" -- "0..1" Multa : pode gerar >
Leitor "1" -- "0..*" Multa : possui >

Bibliotecario "1" -- "0..*" Emprestimo : registra >
Bibliotecario "1" -- "0..*" Livro : cadastra >

ISistemaNotificacao ..> Leitor : notifica >

@enduml
```



### Imagem
![alt text](imgs/Biblioteca.png)
