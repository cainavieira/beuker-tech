---
name: formatar-nota-estudo
description: Compila uma nota bruta de estudo (texto malformado + fotos, escrita pelo usuário a partir de "templates/Template nota bruta tech.md") numa nota tech-study formatada no padrão do vault, linkando/criando as notas de conceito envolvidas e organizando as fotos citadas. Use quando o usuário pedir para "formatar/compilar minha nota de estudo", "transformar o bruto em tech-study", ou apontar um arquivo de nota bruta.
---

# Formatar nota de estudo (bruto → tech-study)

Esta skill lê uma nota bruta de estudo — sempre um arquivo por vez, sempre
chamado `nota bruta tech.md` (case-insensitive) na raiz do vault, escrito
pelo usuário a partir de `templates/Template nota bruta tech.md` — e produz:

1. Uma nota nova em `tech-study-diario/`, no padrão de `templates/template-tech-study.md`.
2. Notas de conceito linkadas (e, se necessário e confirmado, criadas) em `conceitos/`.
3. As fotos citadas no bruto organizadas em `fotos/`, sem nenhum link/embed.
4. O arquivo bruto original apagado ao final.

## Passo 0 — Ler a nota bruta e extrair título e conceitos

- Procure na raiz do vault um arquivo chamado `nota bruta tech.md`
  (case-insensitive — pode estar como `Nota Bruta Tech.md`, etc.). Só existe
  um de cada vez; não é preciso o usuário apontar o nome, o nome é sempre
  esse. Se não achar nenhum, avise e pare.
- Seção `## O que estou estudando (palavras-chave)`: vira o título/nome do
  arquivo da nota tech-study e a base do conteúdo de "O que estudei hoje".
- Seção `## Conceito (ordem de importância)`: cada item é um conceito, na ordem
  em que foi escrito — o primeiro é sempre o principal. A ordem de escrita já é
  a prioridade, não pergunte isso.
- Se a seção `## Estudo` mencionar um conceito que não está listado em
  "Conceito", ou se a lista estiver vazia enquanto o texto claramente fala de
  algo específico, **pare e pergunte** qual conceito usar antes de seguir.
  Nunca infira conceito silenciosamente a partir do texto livre.
- Regras de como casar cada conceito com uma nota existente ou criar uma nova:
  ver `reference/conceitos.md`.

## Passo 1 — Compilar a nota tech-study

- Gere um arquivo **novo** em `tech-study-diario/`, seguindo a estrutura de
  `templates/template-tech-study.md` (frontmatter + seções). Cada sessão de
  estudo é sempre um arquivo novo — nunca edição de uma nota tech-study
  existente.
- Regras de frontmatter, tom de resumo e o que nunca copiar cru do bruto: ver
  `reference/nota-diaria.md`.

## Passo 2 — Organizar as fotos

- Toda foto referenciada no bruto vai para a pasta `fotos/` (raiz do vault, já
  existe — não criar de novo), renomeada e **sem nenhum link/embed** em
  nenhuma nota.
- Regras de nomenclatura e resolução de conflito: ver `reference/fotos.md`.

## Passo 3 — Mostrar o resultado e apagar o bruto

- Mostre ao usuário, na íntegra: a nota tech-study gerada, os conceitos
  criados/linkados e a lista de fotos movidas (nome antigo → novo).
- Só depois de mostrar, apague o arquivo `nota bruta tech.md` original — ele é
  efêmero por design, não serve para mais nada uma vez compilado. Na próxima
  sessão de estudo, o usuário cria um novo `nota bruta tech.md` do zero a
  partir do template.
- **Nunca execute `git add`, `git commit` ou `git push`** como parte desta
  skill.
