# Exercício: Aplicativo de Playlist

## 1. Diagrama de Casos de Uso

Para o sistema de streaming de música, o **Usuário** interage com as funcionalidades relacionadas à pesquisa, organização e reprodução de músicas. Já o **Artista** é responsável pelo cadastro de novas músicas no sistema. As funcionalidades de gerenciamento de playlists ficam associadas ao Usuário, permitindo criar uma playlist, adicionar ou remover músicas e reproduzir seu conteúdo.

### Codigo PlantUML

```plantuml
@startuml
left to right direction

actor Usuario
actor Artista

rectangle "Aplicativo de Streaming de Música" {
    usecase "Pesquisar Música" as UC1
    usecase "Criar Playlist" as UC2
    usecase "Adicionar Música à Playlist" as UC3
    usecase "Remover Música da Playlist" as UC4
    usecase "Reproduzir Playlist" as UC5
    usecase "Cadastrar Música" as UC6
}

Usuario --> UC1
Usuario --> UC2
Usuario --> UC3
Usuario --> UC4
Usuario --> UC5

Artista --> UC6

@enduml
```

![[01.png]]

---

## 2. Diagrama de Classes

O diagrama de classes representa as principais entidades do aplicativo. Um **Usuário** pode possuir várias playlists, enquanto cada **Playlist** pertence a um único usuário. Uma playlist pode conter várias músicas e uma mesma música pode estar presente em várias playlists, caracterizando um relacionamento muitos-para-muitos. Cada **Música** está associada a um único **Artista**, enquanto um artista pode cadastrar várias músicas.

### Codigo PlantUML

```plantuml
@startuml

class Usuario {
    - id: int
    - nome: String
    - email: String
    + criarPlaylist(nome: String): Playlist
    + pesquisarMusica(termo: String): List<Musica>
    + reproduzirPlaylist(playlist: Playlist): void
}

class Playlist {
    - id: int
    - nome: String
    - dataCriacao: Date
    + adicionarMusica(musica: Musica): void
    + removerMusica(musica: Musica): void
    + reproduzir(): void
}

class Musica {
    - id: int
    - titulo: String
    - duracao: int
    - album: String
    + reproduzir(): void
}

class Artista {
    - id: int
    - nome: String
    - genero: String
    + cadastrarMusica(musica: Musica): void
}

Usuario "1" -- "0..*" Playlist : possui
Playlist "0..*" -- "0..*" Musica : contém
Artista "1" -- "0..*" Musica : cadastra

@enduml
```

![[02.png]]

---

## 3. Diagrama de Objetos

O diagrama de objetos apresenta um exemplo concreto do sistema em determinado momento. Neste cenário, o usuário **vinicius : Usuario** possui a playlist **Apenas uma playlist : Playlist**, que contém as músicas **"Hangin' Tough"**, da banda New Kids On The Block, e **"You're the Best Around"**, do artista Joe Esposito. Cada música está associada ao seu respectivo artista.

### Codigo PlantUML

```plantuml
@startuml

object "vinicius : Usuario" as usuario1 {
    id = 1
    nome = "Vinicius"
    email = "Vncs.rambo@gmail.com"
}

object "Apenas uma playlist : Playlist" as playlist1 {
    id = 10
    nome = "Apenas uma playlist"
}

object "hanginTough : Musica" as musica1 {
    id = 101
    titulo = "Hangin' Tough"
    duracao = 243
}

object "youreTheBestAround : Musica" as musica2 {
    id = 102
    titulo = "You're the Best Around"
    duracao = 190
}

object "newKidsOnTheBlock : Artista" as artista1 {
    id = 201
    nome = "New Kids On The Block"
    genero = "Pop"
}

object "joeEsposito : Artista" as artista2 {
    id = 202
    nome = "Joe Esposito"
    genero = "Pop/Rock"
}

usuario1 -- playlist1
playlist1 -- musica1
playlist1 -- musica2
artista1 -- musica1
artista2 -- musica2

@enduml
```

![[03.png]]

---

## 4. Diagrama de Sequência

Para o cenário de **Adicionar Música à Playlist**, o Usuário seleciona uma música pela interface da playlist. A `TelaPlaylist` encaminha a solicitação ao `PlaylistController`, que localiza a playlist e a música e solicita à playlist que realize a associação. Após a operação, o controlador solicita ao Banco de Dados que persista a alteração e retorna a confirmação para a interface.

### Codigo PlantUML

```plantuml
@startuml
skinparam maxMessageSize 150

actor Usuario
boundary TelaPlaylist
control PlaylistController
entity Playlist
entity Musica
database BancoDeDados as BD

Usuario -> TelaPlaylist: selecionarMusica(musicaId)
TelaPlaylist -> PlaylistController: adicionarMusica(playlistId, musicaId)

PlaylistController -> Playlist: buscarPlaylist(playlistId)
Playlist --> PlaylistController: playlist

PlaylistController -> Musica: buscarMusica(musicaId)
Musica --> PlaylistController: musica

PlaylistController -> Playlist: adicionarMusica(musica)
Playlist --> PlaylistController: musicaAdicionada()

PlaylistController -> BD: salvarAlteracao(playlist)
BD --> PlaylistController: confirmacaoSalvamento()

PlaylistController --> TelaPlaylist: confirmacaoAdicao()
TelaPlaylist --> Usuario: apresentarConfirmacao()

@enduml
```

![[04.png]]

---

## 5. Diagrama de Comunicação

O diagrama de comunicação representa o mesmo cenário de adição de uma música à playlist, porém destaca a colaboração entre os objetos envolvidos. As mensagens são numeradas para indicar a ordem em que as operações acontecem, desde a seleção da música pelo usuário até a confirmação da alteração.

### Codigo PlantUML

```plantuml
@startuml

object "usuario : Usuario" as usuario
object "tela : TelaPlaylist" as tela
object "controller : PlaylistController" as controller
object "playlist1 : Playlist" as playlist1
object "musica1 : Musica" as musica1
object "bd : BancoDeDados" as bd

usuario -> tela : 1: selecionarMusica(musicaId)
tela -> controller : 2: adicionarMusica(playlistId, musicaId)

controller -> playlist1 : 3: buscarPlaylist(playlistId)
playlist1 --> controller : 3.1: retornarPlaylist()

controller -> musica1 : 4: buscarMusica(musicaId)
musica1 --> controller : 4.1: retornarMusica()

controller -> playlist1 : 5: adicionarMusica(musica1)
playlist1 --> controller : 5.1: musicaAdicionada()

controller -> bd : 6: salvarAlteracao(playlist1)
bd --> controller : 6.1: confirmacaoSalvamento()

controller --> tela : 7: confirmacaoAdicao()
tela --> usuario : 8: apresentarConfirmacao()

@enduml
```

![[05.png]]
