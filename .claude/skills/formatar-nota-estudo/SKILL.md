---
name: formatar-nota-estudo
description: Processa todas as notas brutas de estudo da raiz (nota bruta tech.md, nota bruta tech 2.md, etc. — texto malformado + fotos, escrito pelo usuário a partir de "templates/Template nota bruta tech.md") em sequência, compilando cada uma numa nota tech-study formatada no padrão do vault, linkando/criando as notas de conceito envolvidas, organizando as fotos marcadas e deletando as não marcadas. Use quando o usuário pedir para "formatar/compilar minhas notas de estudo", "transformar o bruto em tech-study", ou apontar arquivos de nota bruta.
---

# Formatar nota de estudo (bruto → tech-study)

Esta skill processa **todas as notas brutas** que existirem na raiz do vault,
uma por vez.

A estrutura é um laço:

- **Passo 0** levanta a fila de notas brutas — roda uma vez só, no começo.
- **Passos 1 a 4** são o corpo do laço: compilam **uma** nota bruta do início
  ao fim (ler → compilar → fotos → mostrar e limpar). Repetem-se inteiros
  para cada bruto da fila.
- **Passo 5** encerra, quando a fila acaba.

O resultado de cada volta do laço é: uma nota nova em `tech-study-diario/`,
as notas de conceito linkadas (e criadas, se confirmado), as fotos marcadas
organizadas em `fotos/`, e o bruto original apagado.

## Passo 0 — Levantar a fila de notas brutas (uma vez)

- Procure na raiz do vault por arquivos chamados `nota bruta tech.md` (sem número,
  se existir), depois `nota bruta tech 2.md`, `nota bruta tech 3.md`, etc.,
  em ordem sequencial (case-insensitive). Se não achar nenhum, avise e pare.
- Essa é a fila. Processe um bruto de cada vez pelos Passos 1 a 4, na ordem,
  e só passe para o próximo quando o anterior estiver concluído e limpo.

## Passo 1 — Ler o bruto: título e conceitos

- **Ignore os comentários do template.** O bruto vem de
  `templates/Template nota bruta tech.md`, que traz instruções em blocos
  `<!-- ... -->` sob cada título. Esses blocos são ajuda para o usuário, não
  conteúdo dele — nunca os trate como matéria de estudo, nunca os copie para
  a nota. O conteúdo real é o que o usuário escreveu **fora** deles,
  normalmente logo abaixo, às vezes indentado (indentação aí é acidente de
  digitação, não bloco de código — não a preserve).
- Seção `## O que estou estudando`: texto livre (palavras-chave soltas ou
  frase inteira, do jeito que o usuário escreveu no calor do estudo). Nunca
  use cru como nome de arquivo: derive dela um título legível, **proponha e
  confirme com o usuário** antes de criar a nota, e registre o resultado no
  histórico de `reference/titulos.md` — é de lá que sai o estilo de título.
  Essa seção também é a base do conteúdo de 📚 "O que estudei hoje".
- Seção `## Conceito (ordem de importância)`: cada item da lista é um
  conceito, e os itens podem vir separados por `/` numa linha só. A ordem em
  que foram escritos já é a prioridade — o primeiro é sempre o principal.
  Não pergunte sobre ordem.
- Se a seção `## Estudo` mencionar um conceito que não está listado em
  "Conceito", ou se a lista estiver vazia enquanto o texto claramente fala de
  algo específico, **pare e pergunte** qual conceito usar antes de seguir.
  Nunca infira conceito silenciosamente a partir do texto livre.
- Regras de como casar cada conceito com uma nota existente ou criar uma nova:
  ver `reference/conceitos.md`. Regras de título e confirmação: ver
  `reference/titulos.md`.
- **Junte as perguntas numa só interação.** Se precisar confirmar título e
  também perguntar sobre conceito, pergunte as duas coisas de uma vez antes de
  começar a compilar — o usuário não deve ser interrompido duas vezes na mesma
  sessão.

## Passo 2 — Compilar a nota tech-study

- Gere um arquivo **novo** em `tech-study-diario/`, seguindo a estrutura de
  `templates/template-tech-study.md` (frontmatter + seções). Cada sessão é
  sempre um arquivo novo. A única exceção é o usuário pedir explicitamente
  para editar uma nota já existente, apontando o `id_obsidian` dela.
- Reescreva o conteúdo do bruto para ficar claro, conciso e explicativo.
  **Nunca copie cru.**
- **Melhorar o material é permitido; inventar não.** Deixar mais clara uma
  explicação confusa, corrigir um erro factual do bruto, tornar explícita uma
  conexão que ficou implícita, completar a sintaxe de um comando citado pela
  metade — tudo isso é melhoria legítima, porque continua **dentro do que a
  sessão cobriu**. O que não pode é ampliar o escopo: puxar assunto que o
  usuário não estudou, ou encher seção rasa com definição genérica de
  documentação. A fronteira exata, com exemplos dos dois lados, está em
  "Melhorar sim, inventar não" (`reference/nota-diaria.md`).
- A nota é material de revisão, não registro de que a sessão aconteceu: o
  usuário vai reler isso meses depois sem lembrar da aula. Por isso 📖
  "Conteúdo" carrega a matéria explicada (📚 é só o escopo) e ❓ "Autoteste"
  fecha a nota com perguntas de recuperação ativa. Seção opcional sem
  conteúdo real é omitida inteira, não fica com bullet vazio.
- **Links são a única exceção à reescrita**: qualquer URL colada no bruto
  (solta ou em markdown) sobrevive exata, caractere por caractere, mesmo
  dentro de um trecho que está sendo resumido/reescrito — nunca parafraseie,
  encurte ou "limpe" um link. Ver "Links sobrevivem sempre intactos" em
  `reference/nota-diaria.md`.
- Regras de frontmatter, formato de cada seção e tom do resumo: ver
  `reference/nota-diaria.md`.
- **Leia `reference/exemplo.md` antes de escrever a nota**: é um par completo
  bruto → nota que fixa o nível de detalhe esperado em cada seção. Imite a
  forma, nunca o conteúdo (o assunto de lá é Docker por acaso).

## Passo 3 — Organizar as fotos

- Toda foto do bruto é **material de estudo**: abra cada imagem, leia o que
  está nela e use isso para escrever as seções — principalmente 📖
  "Conteúdo", e 🐞 "Erros e como resolvi" quando for print de erro. Isso vale
  para **todas** as fotos, marcadas ou não; muitas vezes a foto é a única
  fonte de um detalhe.
- A marcação (`salvar`, ou `salvar: legenda`, na linha logo abaixo da foto)
  decide apenas se a imagem **também** é guardada e embedada na nota. Sem
  marcação, o arquivo é apagado no Passo 4 e o aprendizado sobrevive só no
  texto. Nunca embede por conta própria; se a marcação for ambígua, pergunte.
- **Regras completas em `reference/fotos.md`** (nomenclatura, marcação, alt,
  sintaxe e em que seção colocar o embed). Leia esse arquivo se o bruto tiver
  ao menos uma foto; se não tiver nenhuma, pule o passo.

## Passo 4 — Mostrar o resultado e limpar

- Mostre ao usuário, na íntegra: a nota tech-study gerada nesta volta do laço,
  os conceitos criados/linkados e a lista de fotos salvas (nome antigo → novo),
  marcando em que seção cada uma foi embedada.
- Só depois de mostrar, limpe:
  - Apague o arquivo bruto desta volta (é efêmero por design).
  - Delete da raiz do vault apenas as fotos **citadas neste bruto** (o mesmo
    conjunto identificado no Passo 3) que não foram marcadas para salvar —
    foram lidas pro conteúdo, mas não precisam ficar guardadas. Nunca apague
    outra imagem da raiz que não esteja referenciada neste bruto específico
    (foto de outro bruto ainda não processado, print solto, etc.).
- Se ainda houver bruto na fila do Passo 0, volte ao **Passo 1** com o
  próximo. Se a fila acabou, siga para o Passo 5.

## Passo 5 — Finalizar

- Mostre um resumo final: quantas notas foram compiladas nesta sessão,
  quantas notas de conceito foram criadas, e os títulos usados.
- **Nunca execute `git add`, `git commit` ou `git push`** como parte desta
  skill.
