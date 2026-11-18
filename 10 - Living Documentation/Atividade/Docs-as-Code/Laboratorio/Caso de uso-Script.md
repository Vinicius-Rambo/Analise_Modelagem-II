# UC01 — Cadastrar tarefa

**Sistema:** Lista de Tarefas  
**Desenvolvido por:** VRambo  
**Versão:** 1.0

## 1\. Apresentação

Este caso de uso descreve como um **usuário** cadastra uma tarefa para organizar suas atividades. A tarefa é criada com o estado *pendente*.

O documento apresenta as condições para iniciar o cadastro, a sequência de interação com o sistema e o tratamento de um título vazio.

> Este caso de uso começa com o usuário na tela de tarefas.

## 2\. Identificação

| Informação | Descrição |
| :---- | :---- |
| Código | `UC01` |
| Nome | Cadastrar tarefa |
| Ator principal | Usuário |
| Objetivo | Registrar uma atividade a realizar |
| Gatilho | Usuário seleciona “Nova tarefa” |

## 3\. Precondições

- O sistema está disponível.  
- O usuário está na tela de tarefas.

## 4\. Regras de Negócio

O ***título é obrigatório***. A descrição é opcional.

Regra substituída: ~~A descrição deve ser obrigatória.~~

| Campo | Obrigatório | Limite de caracteres |
| :---- | :---: | ----: |
| Título | Sim | 100 |
| Descrição | Não | 500 |

Os limites são verificados após a remoção dos espaços no início e no fim dos textos. Um título composto somente por espaços é considerado vazio.

> Orientação de preenchimento:

> > Use um título curto e explícito que identifique a atividade.

## 5\. Fluxos do caso de uso

### 5.1. Fluxo principal

1. O usuário seleciona **Nova tarefa**.  
2. O sistema apresenta o formulário de cadastro.  
3. O usuário preenche os campos:  
   - `titulo`: “Estudar Markdown”.  
   - `descricao`: “Concluir o laboratório de documentação”.  
4. O usuário seleciona **Salvar**.  
5. O sistema valida as regras de preenchimento.  
6. O sistema registra a tarefa com o estado *pendente*.  
7. O sistema exibe a tarefa na lista e apresenta a mensagem `Tarefa cadastrada com sucesso`.

### 5.2. Fluxos alternativos

#### 5.2.1. A1 — Título vazio

Na etapa 5, o sistema identifica que o título está vazio e não cadastra a tarefa.

##### Tratamento

O sistema mantém os dados preenchidos e solicita a correção do título.

###### *Mensagem apresentada*

`Informe o título da tarefa.`

Após a correção, o usuário retoma o fluxo principal na etapa 4\.

#### 5.2.2. A2 — Limite de caracteres excedido

Na etapa 5, o sistema identifica um campo acima do limite, não cadastra a tarefa e informa qual campo deve ser reduzido. Após a correção, o usuário retoma o fluxo na etapa 4\.

## 6\. Pós-condições

1. Em caso de sucesso:  
   - A tarefa está **registrada**.  
   - O estado inicial é `pendente`.  
   - A tarefa aparece na *lista*.  
2. Enquanto **houver erro** de validação:  
   - Nenhuma tarefa é cadastrada.  
   - Os dados permanecem disponíveis para correção.

## 7\. Exemplos técnicos

### 7.1. Dados de uma tarefa cadastrada

O campo `concluida` recebe `false` quando a tarefa está pendente.

```json
{
  "id": 1,
  "titulo": "Estudar Markdown",
  "descricao": "Concluir o laboratório de documentação",
  "concluida": false
}
```

### 7.2. Validação ilustrativa do título

Este trecho demonstra somente a validação do título; ele não implementa o sistema completo.

```py
def validar_titulo(titulo):
    titulo = titulo.strip()
    if not titulo:
]
        return "Informe o título da tarefa."
    if len(titulo) > 100:
        return "O título deve ter até 100 caracteres."
    return "Título válido."
```

8\. Material de apoio do Laboratório

![Símbolo do Markdown: letra M acompanhada de seta para baixo][image1]

Consulte a [referência de Markdown do CommonMark](https://commonmark.org/help/).

[image1]: <data:image/png;base64,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>