# Regras de compilação da nota tech-study

## Frontmatter

- `tipo: tech-study`
- `data:` — data real da sessão (hoje, a menos que o bruto deixe claro outra
  data).
- `tags: [tech-study]`
- `conceito:` — wikilink do conceito principal (primeiro item da lista do
  bruto).
- `objetivo: "[[Objetivos Tech Pessoal]]"` — mantém fixo, igual ao template.

## Corpo — tom de resumo

- **Nunca copie o bruto cru.** O objetivo é resumir e organizar, não
  transcrever. Bullets soltos e mal formatados do bruto viram frases coesas
  nas seções certas.
- **📚 O que estudei hoje**: parte da seção "O que estou estudando
  (palavras-chave)" do bruto — reescreva como `[[Conceito]] — o que foi
  feito`, um item por conceito tocado na sessão.
- **💡 Aprendizados / insights**: só o que for aprendizado real (algo que o
  usuário não sabia antes ou uma conexão nova) — não é resumo de tudo que foi
  lido.
- **🧠 Dúvidas / pontos a aprofundar**: dúvidas reais que apareceram no bruto,
  nunca invente nem deixe genérico tipo "revisar depois" sem contexto.
- **🔗 Recursos usados**: links/nomes de fontes citadas no bruto (docs,
  vídeos, repositórios).
- **🔁 Próximos passos**: só se o bruto indicar algo concreto a seguir; se não
  houver nada claro, deixe a seção vazia — não invente próximo passo.
- **🗒️ Observações gerais**: qualquer coisa relevante que não caiba nas
  seções acima.

## Identificação (id_obsidian / id_pai)

- Toda nota tech-study recebe `id_obsidian`, gerado no momento da criação da
  nota, formato `YYYYMMDD-HHMMSS` (data e hora local de criação, até o
  segundo — necessário porque a skill costuma criar conceito(s) e a nota
  tech-study quase no mesmo instante, e colisão por minuto é comum). Se por
  acaso colidir com um `id_obsidian` já existente (duas notas no mesmo
  segundo), acrescente sufixo `-2`, `-3`...
- `id_pai` recebe o `id_obsidian` já existente no frontmatter do conceito
  principal (o mesmo que vai em `conceito:` — primeiro item da lista do
  bruto). **Nunca infira ou gere esse ID por conta própria** — ele sempre
  vem do arquivo de conceito já resolvido pelo processo de match/criação de
  `reference/conceitos.md`; o conceito em si é sempre o que o usuário
  escreveu no bruto, nunca inferido do texto livre.

## Zona auto-gerada

- Cada seção (📚, 💡, 🧠, 🔗, 🔁, 🗒️) tem seu **próprio** par de marcadores
  `--- INÍCIO AUTO-GERADO ---` / `--- FIM AUTO-GERADO ---` no template — não
  é um bloco único cobrindo a nota inteira. A skill só escreve dentro desses
  marcadores, título da seção (`##`) sempre fora.
- Isso deixa espaço pro usuário escrever manualmente dentro da mesma seção,
  fora do par de marcadores dela (ex.: acrescentar uma linha própria embaixo
  do `--- FIM AUTO-GERADO ---` de "💡 Aprendizados / insights", ainda dentro
  dessa seção). Esse conteúdo nunca deve ser tocado.
- Ao gerar a nota pela primeira vez, preencha só o miolo de cada bloco (entre
  os marcadores daquela seção), mantendo os marcadores intactos.
- A seção `## ✍️ Notas minhas`, no fim do arquivo e sem marcadores, é criada
  vazia e nunca preenchida pela skill — espaço livre genérico, fora de
  qualquer seção específica.
- Se o usuário pedir uma edição numa nota tech-study já existente (apontando
  pelo `id_obsidian`), localize a seção certa e só altere o conteúdo entre o
  par de marcadores **daquela seção**; tudo fora de marcadores, em qualquer
  seção, fica intocado.

## Nome e local do arquivo

- O nome do arquivo é a seção "O que estou estudando (palavras-chave)" do
  bruto, como escrita (só sanitize caracteres inválidos de nome de arquivo —
  `\ / : * ? " < > |` — mantendo acentos, espaços e maiúsculas como o usuário
  escreveu). Data e conceito já estão no frontmatter, não precisam repetir no
  nome.
- `tech-study-diario/<o que estou estudando>.md` (ex.:
  `tech-study-diario/Debug de skills do Claude Code.md`).
- Se já existir um arquivo com esse nome (ex.: duas sessões com o mesmo
  título), acrescente sufixo `-2`, `-3`... nunca sobrescreva uma sessão
  anterior.
