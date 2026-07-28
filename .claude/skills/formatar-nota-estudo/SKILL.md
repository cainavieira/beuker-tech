---
name: formatar-nota-estudo
description: Processa todas as notas brutas de estudo da raiz (nota bruta tech.md, nota bruta tech 2.md, etc. — texto malformado + fotos, escrito pelo usuário a partir de "templates/Template nota bruta tech.md") em sequência, compilando cada uma numa nota tech-study formatada no padrão do vault, linkando/criando as notas de conceito envolvidas e organizando as fotos citadas. Use quando o usuário pedir para "formatar/compilar minhas notas de estudo", "transformar o bruto em tech-study", ou apontar arquivos de nota bruta.
---

# Formatar nota de estudo (bruto → tech-study)

Esta skill processa **todas as notas brutas** que existirem na raiz do vault.
Para cada uma, lê, compila numa nota tech-study, organiza fotos, e apaga o bruto.
O processamento é sequencial (uma por vez), em ordem numérica:
`nota bruta tech.md`, depois `nota bruta tech 2.md`, `nota bruta tech 3.md`, etc.

Para cada nota bruta processada:

1. Uma nota nova em `tech-study-diario/`, no padrão de `templates/template-tech-study.md`.
2. Notas de conceito linkadas (e, se necessário e confirmado, criadas) em `conceitos/`.
3. As fotos citadas no bruto lidas e usadas como conteúdo da nota, organizadas
   em `fotos/`, e embedadas na nota apenas quando o usuário marcou.
4. O arquivo bruto original apagado ao final.

## Passo 0 — Encontrar e processar todas as notas brutas

- Procure na raiz do vault por arquivos chamados `nota bruta tech.md` (sem número,
  se existir), depois `nota bruta tech 2.md`, `nota bruta tech 3.md`, etc.,
  em ordem sequencial (case-insensitive). Se não achar nenhum, avise e pare.
- Para cada nota bruta encontrada, processe-a pelos passos 0b–3 abaixo antes de
  passar pra próxima. Ao final de cada uma, mostre os resultados dessa sessão.

## Passo 0b — Ler a nota bruta e extrair título e conceitos

- Seção `## O que estou estudando`: texto livre (palavras-chave soltas ou
  frase inteira, do jeito que o usuário escreveu no calor do estudo). Nunca
  use cru como nome de arquivo: derive dela um título legível, **proponha e
  confirme com o usuário** antes de criar a nota, e registre o resultado no
  histórico de `reference/titulos.md` — é de lá que sai o estilo de título.
  Essa seção também é a base do conteúdo de 📚 "O que estudei hoje".
- Seção `## Conceito (ordem de importância)`: cada item é um conceito, na ordem
  em que foi escrito separado por um "/", porém o primeiro é sempre o principal. A ordem de escrita já é
  a prioridade, não pergunte isso.
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

## Passo 1 — Compilar a nota tech-study

- Gere um arquivo **novo** em `tech-study-diario/`, seguindo a estrutura de
  `templates/template-tech-study.md` (frontmatter + seções). Cada sessão de
  estudo é sempre um arquivo novo — nunca edição de uma nota tech-study
  existente a menos que o usuário peça explicitamente para editar uma nota já existente, apontando pelo `id_obsidian` dela.
- Preencha cada seção com o conteúdo do bruto, **reescrevendo** e resumindo ou até sugerindo melhorias de forma a ficar mais claro, conciso, legivel e explicativo, mas **nunca copie cru** do bruto.
- A nota é material de revisão, não registro de que a sessão aconteceu: o
  usuário vai reler isso meses depois sem lembrar da aula. Por isso 📖
  "Conteúdo" carrega a matéria explicada (📚 é só o escopo) e ❓ "Autoteste"
  fecha a nota com perguntas de recuperação ativa. Seção opcional sem
  conteúdo real é omitida inteira, não fica com bullet vazio.
- As fotos do bruto são conteúdo, não anexo: abra cada imagem, leia o que está
  nela e use isso para escrever as seções (principalmente 📖), do mesmo
  jeito que o texto do bruto. Nenhuma foto é só arquivada sem passar por aqui
  — ver `reference/fotos.md`.
- Regras de frontmatter, tom de resumo bem feito e explicativo mas nunca copiar cru do bruto: ver
  `reference/nota-diaria.md`.
- **Leia `reference/exemplo.md` antes de escrever a nota**: é um par completo
  bruto → nota que fixa o nível de detalhe esperado em cada seção. Imite a
  forma, nunca o conteúdo (o assunto de lá é Docker por acaso).

## Passo 2 — Organizar as fotos

- Toda foto referenciada no bruto vai para a pasta `fotos/` (raiz do vault, já
  existe — não criar de novo), renomeada.
- **Embed só nas fotos marcadas**: se o usuário escreveu uma marcação
  explícita (`salvar`, opcionalmente `salvar: legenda`) na linha logo abaixo
  da foto no bruto, essa foto também entra na nota como link markdown
  `![alt](<fotos/nome novo.ext>)`, dentro dos marcadores auto-gerados da seção
  que trata do assunto. Foto sem marcação vai só para `fotos/`, sem link.
  Nunca embede por conta própria; se a marcação for ambígua, pergunte.
- Regras de nomenclatura, marcação, sintaxe e posição do embed: ver
  `reference/fotos.md`.

## Passo 3 — Mostrar o resultado e apagar o bruto (para cada nota)

- Mostre ao usuário, na íntegra: a nota tech-study gerada dessa iteração,
  os conceitos criados/linkados e a lista de fotos movidas (nome antigo → novo),
  marcando quais foram embedadas na nota e em que seção, e quais só foram arquivadas.
- Só depois de mostrar, apague o arquivo bruto original dessa iteração — ele é
  efêmero por design, não serve para mais nada uma vez compilado.
- Depois, volte ao **Passo 0**: procure pela próxima nota bruta sequencialmente
  e repita o ciclo (Passo 0b–3) para ela. Continue até não achar mais notas brutas.

## Passo 4 — Finalizar (quando não houver mais notas brutas)

- Quando procurar pela próxima nota bruta e não encontrar nenhuma, a skill termina.
- Mostre um resumo final: quantas notas foram compiladas nesta sessão, quantas
  notas de conceito foram criadas, e pronto.
- **Nunca execute `git add`, `git commit` ou `git push`** como parte desta
  skill.
