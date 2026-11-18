# Roteiro — laboratório de MkDocs

**Ambiente:** Ubuntu 24.04, sem acesso ao root e sem uso de `sudo`.

**Objetivo:** aproveitar o conteúdo Markdown criado na atividade anterior, organizá-lo em páginas e gerar um site de documentação. Ao final, haverá uma demonstração extra de como servir os arquivos gerados usando Python.&nbsp;

## 1\. Conferir o ambiente

No terminal:

```sh
python3 --version
python3 -m venv --help
```

Se o segundo comando falhar, ou se o `pip` não estiver disponível, avisar o responsável pelo laboratório. Sem acesso ao root, não será possível instalar pacotes do sistema com `apt`; por isso, Python, `venv` e `pip` precisam estar preparados antes da aula.

## 2\. Criar a pasta e o ambiente virtual

```sh
mkdir -p ~/laboratorio-mkdocs
cd ~/laboratorio-mkdocs

python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install mkdocs
```

O ambiente virtual instala o MkDocs dentro da pasta do projeto, sem modificar os pacotes globais do sistema. Não usar `sudo`.

Se a instalação não funcionar por falta de rede ou bloqueio do repositório de pacotes, resolver isso com o responsável pelo laboratório antes de continuar.

## 3\. Criar a estrutura do site

Criar a pasta que vai conter as páginas:

```sh
mkdir docs
```

Na pasta principal `laboratorio-mkdocs/`, criar o arquivo `mkdocs.yml`:

&nbsp;

```
site_name: Sistema de Biblioteca

theme:
  name: readthedocs

nav:
  - Início: index.md
  - Funcionalidades: funcionalidades.md
  - Instalação: instalacao.md

repo_url: https://github.com/Vinicius-Rambo/O.Objetos-II

```

&nbsp;

Dentro de `docs/`, criar `index.md`:

&nbsp;

```
# Sistema de Biblioteca

Este projeto fictício organiza o cadastro de livros e o controle de empréstimos.

## Objetivo

Facilitar a consulta de livros e o acompanhamento dos empréstimos.
```

&nbsp;

Criar `docs/funcionalidades.md`:

&nbsp;

```
# Funcionalidades

- Cadastrar e consultar livros.
- Cadastrar usuários.
- Registrar empréstimos e devoluções.

| Funcionalidade | Situação |
| --- | --- |
| Cadastro de livros | Planejada |
| Empréstimos | Em desenvolvimento |
```

&nbsp;

Criar `docs/instalacao.md`:

&nbsp;

```
# Instalação

Estes passos são um exemplo para o projeto fictício.

1. Obtenha os arquivos do projeto.
2. Instale as dependências da aplicação.
3. Configure o ambiente.
4. Execute a aplicação conforme as instruções do projeto.
```

&nbsp;

Se os alunos já tiverem um documento criado no laboratório de Markdown, podem reaproveitá-lo em `index.md` e separar o restante do conteúdo em páginas. O importante é que os nomes no `nav` correspondam aos arquivos existentes em `docs/`.

A estrutura esperada:

```
laboratorio-mkdocs/
├── .venv/
├── mkdocs.yml
└── docs/
    ├── index.md
    ├── funcionalidades.md
    └── instalacao.md
```

## 4\. Visualizar o site

Na pasta onde está `mkdocs.yml`, com o ambiente virtual ativo, executar:

```sh
mkdocs serve
```

Abrir no navegador o endereço informado pelo terminal. Normalmente é:

```
http://127.0.0.1:8000/
```

Mostrar o menu e abrir as páginas. Em seguida, editar uma frase em `docs/index.md`, salvar e conferir a atualização no navegador.

Para encerrar o servidor do MkDocs, pressionar `Ctrl+C`.

## 5\. Gerar os arquivos finais

Executar:

```sh
mkdocs build
```

O MkDocs cria a pasta `site/`. Ela contém o resultado pronto para ser servido ou publicado: não é necessário manter o comando `mkdocs serve` rodando para usar essa versão gerada.

## 6\. Demonstração extra: servir a pasta `site/` com Python

**Esta parte é uma demonstração do apresentador; os alunos não precisam executá-la.**

Explicar que o MkDocs gera arquivos estáticos. Depois que a pasta `site/` existe, qualquer servidor HTTP capaz de entregar arquivos estáticos pode disponibilizá-la. Para demonstrar isso sem instalar outra ferramenta, usar o servidor simples que já vem com o Python.

Na raiz do projeto, executar:

```sh
python3 -m http.server 8000 --directory site
```

Abrir no navegador:

```
http://127.0.0.1:8000/
```

O conteúdo deve aparecer como o site gerado pelo MkDocs, mas agora está sendo servido pelo módulo HTTP do Python, e não pelo servidor de desenvolvimento do MkDocs.

Para encerrar, pressionar `Ctrl+C`.

**Diferença importante:**

- `mkdocs serve`: servidor de desenvolvimento do MkDocs, útil enquanto a documentação está sendo editada.  
- `mkdocs build`: gera os arquivos estáticos na pasta `site/`.  
- `python3 -m http.server 8000 --directory site`: apenas entrega os arquivos que já foram gerados. Não reconstrói o site quando o Markdown muda.

O servidor HTTP do Python é adequado para uma demonstração local, mas não deve ser apresentado como uma solução de hospedagem de produção.

## 7\. Encerrar o ambiente virtual

Quando terminar:

```sh
deactivate
```

Para retomar o trabalho depois:

```sh
cd ~/laboratorio-mkdocs
source .venv/bin/activate
```

## Problemas comuns

- **`venv` não está disponível:** pedir ao responsável que prepare o ambiente antes da aula.  
- **A instalação do MkDocs falha:** conferir a conexão e possíveis bloqueios de rede.  
- **`mkdocs` não é encontrado:** ativar o ambiente com `source .venv/bin/activate`.  
- **A página não abre:** conferir se o servidor continua rodando e usar o endereço informado no terminal.  
- **A pasta `site/` não existe:** executar `mkdocs build` antes de iniciar o servidor Python.