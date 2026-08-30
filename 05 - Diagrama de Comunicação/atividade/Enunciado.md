# **Exercício: Aplicativo de Playlist**

Considere o desenvolvimento de um **aplicativo de streaming** **de música**, semelhante ao Spotify, que permita aos usuários pesquisar músicas, criar playlists e organizar suas músicas favoritas.

O sistema possui dois atores principais:

* **Usuário**;  
* **Artista**.

O usuário pode pesquisar músicas, criar playlists, adicionar ou remover músicas de uma playlist e reproduzi-las. O artista pode cadastrar músicas no sistema.

Considere que:

* um usuário pode possuir várias playlists;  
* uma playlist pode conter várias músicas;  
* uma música pode estar presente em várias playlists;  
* cada música está associada a um artista.

## **Atividade**

Utilizando **UML e PlantUML**, modele o sistema criando os seguintes diagramas:

### **1\. Diagrama de Casos de Uso**

Represente os atores e as principais funcionalidades do sistema:

* Pesquisar Música;  
* Criar Playlist;  
* Adicionar Música à Playlist;  
* Remover Música da Playlist;  
* Reproduzir Playlist;  
* Cadastrar Música.

### **2\. Diagrama de Classes**

Crie as principais classes do sistema:

* `Usuario`;  
* `Playlist`;  
* `Musica`;  
* `Artista`.

Defina alguns atributos, operações e os relacionamentos entre as classes, incluindo suas multiplicidades.

### **3\. Diagrama de Objetos**

Crie um exemplo concreto do sistema utilizando instâncias das classes.

Por exemplo:

* um usuário;  
* uma playlist criada por esse usuário;  
* duas músicas adicionadas à playlist;  
* os respectivos artistas das músicas.

Utilize a notação:

```
nomeDoObjeto : NomeDaClasse
```

### **4\. Diagrama de Sequência**

Modele o cenário:

> **Adicionar Música à Playlist**

Considere os seguintes participantes:

* `Usuario`;  
* `TelaPlaylist`;  
* `PlaylistController`;  
* `Playlist`;  
* `Musica`;  
* `BancoDeDados`.

Represente a sequência de mensagens desde a ação do usuário até a confirmação da operação.

### **5\. Diagrama de Comunicação**

Represente o **mesmo cenário do Diagrama de Sequência**, mostrando a colaboração entre os objetos.

Utilize objetos como:

```
usuario : Usuario
tela : TelaPlaylist
controller : PlaylistController
playlist1 : Playlist
musica1 : Musica
```

As mensagens devem ser **numeradas**, indicando a ordem da interação.