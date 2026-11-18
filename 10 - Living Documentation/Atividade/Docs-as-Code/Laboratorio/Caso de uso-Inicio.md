UC01 — Cadastrar tarefa

Sistema: Lista de Tarefas Desenvolvido por: VRambo Versão: 1.0

1\. Apresentação

Este caso de uso descreve como um usuário cadastra uma tarefa para organizar suas atividades. A tarefa é criada com o estado pendente.

O documento apresenta as condições para iniciar o cadastro, a sequência de interação com o sistema e o tratamento de um título vazio.

Este caso de uso começa com o usuário na tela de tarefas.

2\. Identificação

Informação  Descrição

Código UC01 Nome  Cadastrar tarefa Ator principal  Usuário Objetivo  Registrar uma atividade a realizar Gatilho  Usuário seleciona “Nova tarefa”

3\. Precondições

O sistema está disponível. O usuário está na tela de tarefas.

4\. Regras de Negócio

O título é obrigatório. A descrição é opcional.

Regra substituída: A descrição deve ser obrigatória.

Campo Obrigatório Limite de caracteres

Título  Sim  100&nbsp;

Descrição  Não  500

Os limites são verificados após a remoção dos espaços no início e no fim dos textos. Um título composto somente por espaços é considerado vazio.

Orientação de preenchimento:

Use um título curto e explícito que identifique a atividade.

5\. Fluxos do caso de uso

5.1. Fluxo principal

O usuário seleciona Nova tarefa.&nbsp;

O sistema apresenta o formulário de cadastro.&nbsp;

O usuário preenche os campos: titulo: “Estudar Markdown”. descricao: “Concluir o laboratório de documentação”.

O usuário seleciona Salvar.&nbsp;

O sistema valida as regras de preenchimento.&nbsp;

O sistema registra a tarefa com o estado pendente.&nbsp;

O sistema exibe a tarefa na lista e apresenta a mensagem Tarefa cadastrada com sucesso

5.2. Fluxos alternativos

5.2.1. A1 — Título vazio

Na etapa 5, o sistema identifica que o título está vazio e não cadastra a tarefa.

Tratamento

O sistema mantém os dados preenchidos e solicita a correção do título.

Mensagem apresentada

Informe o título da tarefa.

Após a correção, o usuário retoma o fluxo principal na etapa 4\.

5.2.2. A2 — Limite de caracteres excedido

Na etapa 5, o sistema identifica um campo acima do limite, não cadastra a tarefa e informa qual campo deve ser reduzido. Após a correção, o usuário retoma o fluxo na etapa 4\.

6 Pós-condições

Em caso de sucesso: A tarefa está registrada. O estado inicial é pendente. A tarefa aparece na lista. Enquanto houver erro de validação: Nenhuma tarefa é cadastrada. Os dados permanecem disponíveis para correção.

7 Exemplos técnicos

7.1. Dados de uma tarefa cadastrada

O campo concluida recebe false quando a tarefa está pendente.

json { "id": 1, "titulo": "Estudar Markdown", "descricao": "Concluir o laboratório de documentação", "concluida": false }

7.2. Validação ilustrativa do título

Este trecho demonstra somente a validação do título; ele não implementa o sistema completo.

def validar\_titulo(titulo): titulo \= titulo.strip() if not titulo: return "Informe o título da tarefa." if len(titulo) \> 100: return "O título deve ter até 100 caracteres." return "Título válido."

8\. Material de apoio do Laboratório

[https\://commonmark.org/help/images/favicon.png](https://commonmark.org/help/images/favicon.png)

[https\://commonmark.org/help/](https://commonmark.org/help/)