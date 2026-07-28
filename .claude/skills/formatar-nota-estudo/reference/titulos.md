# Título da nota tech-study

## O campo de origem é livre

O campo `## O que estou estudando` do bruto (em brutos antigos pode aparecer
como `## O que estou estudando (palavras-chave)` — aceite os dois) é **texto
livre**: pode ser palavra-chave solta (`docker comandos, containers`), frase
inteira (`hoje vi como container difere de imagem`), ou qualquer coisa no
meio. O usuário escreve isso durante o estudo, sem pensar em nome de arquivo
— a responsabilidade de virar um título legível é da skill, não dele.

Nunca use o campo cru como nome de arquivo.

## Como derivar o título

- **Frase nominal curta**, 3 a 8 palavras, descrevendo o assunto da sessão.
  Nem pergunta, nem verbo em primeira pessoa: `Comandos Docker e ciclo de
  vida de containers`, não `O que eu estudei de Docker hoje` nem `Como usar
  Docker?`.
- **Sentence case**: só a primeira letra maiúscula, mais nomes próprios e
  tecnologias com a grafia oficial (`Docker`, `Java`, `Linux`, `Azure
  DevOps`) — mesmo que o usuário tenha escrito minúsculo no bruto. Não use
  Title Case Em Todas As Palavras.
- **Sem** data, sem emoji, sem prefixo/sufixo de processo (`estudo de`,
  `sessão`, `aula`, `notas sobre`). A data já está no frontmatter.
- Pode nomear o conceito quando ele é o assunto (`Comandos Docker` é bom) —
  o que não pode é o título ser só o nome do conceito (`Docker`), porque não
  distingue essa sessão das próximas sobre o mesmo conceito.
- **Só use o que está no bruto.** O título resume o que a sessão de fato
  cobriu; não amplie o escopo para soar melhor.
- Sanitize caracteres inválidos de nome de arquivo (`\ / : * ? " < > |`),
  mantendo acentos, espaços e maiúsculas.

## Confirmação com o usuário

- Proponha o título e **peça confirmação antes de criar o arquivo**, sempre
  oferecendo a opção de ele escrever outro. Se houver também alguma pergunta
  sobre conceito (ver `reference/conceitos.md`), faça as duas de uma vez — uma
  interrupção só, não duas.
- Se o usuário corrigir, use o dele **exatamente como escrito** (só
  sanitizando caracteres inválidos) e registre a correção no histórico abaixo.
- Se ele aceitar sem mudar nada, registre também: aceitação é sinal de estilo
  tanto quanto correção.

## Quando parar de perguntar

A confirmação existe para calibrar o gosto do usuário, não para sempre. Assim
que o histórico tiver **5 títulos consecutivos aceitos sem nenhuma
correção**, pare de bloquear: proponha o título, siga em frente e mostre qual
foi no resumo final do Passo 3, para ele contestar se quiser. Se em algum
momento ele corrigir um título de novo, a contagem zera e a confirmação volta
a ser obrigatória.

## Histórico de títulos

Acrescente uma linha por sessão compilada, sempre ao final da tabela. É a
memória de estilo da skill — leia antes de propor um título e siga o padrão
que emergir daqui, mesmo que contrarie as regras genéricas acima (o gosto
registrado do usuário ganha das regras).

| Campo do bruto | Título proposto | Título final | Aceito sem correção? |
| --- | --- | --- | --- |
| Java tipagem, tipos de dados, e variaveis. | Tipos primitivos, variáveis e conversões em Java | Tipos primitivos, variáveis e conversões em Java | Sim |
