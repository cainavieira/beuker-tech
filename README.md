# Study Tech Pessoal

Vault de Obsidian pra organizar anotações de estudo de tecnologia, com duas
skills de [Claude Code](https://claude.com/claude-code) que transformam
anotações cruas (feitas correndo, sem tempo pra formatar) em notas
organizadas automaticamente.

## Por quê

Durante uma aula ou estudo prático, prestar atenção no conteúdo (ex.:
código na tela) e ao mesmo tempo escrever notas bonitas e bem formatadas
competem pelo mesmo tempo. A ideia aqui é separar as duas coisas: você
anota tudo cru, rápido e feio, e a IA formata depois.

## Requisitos

- [Obsidian](https://obsidian.md/) pra navegar/editar o vault.
- [Claude Code](https://claude.com/claude-code) instalado e rodando dentro
  da pasta do vault — é ele quem executa a skill de formatação.

## Estrutura

- `Objetivos Tech Pessoal.md` — objetivos de longo prazo, o "aonde quero
  chegar".
- `moc areas/` — mapas de área (ex.: DevOps, IA), cada um só linkando os
  conceitos que pertencem a ela.
- `conceitos/` — uma nota por conceito de estudo (ex.: "Claude IA", "Docker"),
  que acumula várias sessões de estudo ao longo do tempo.
- `tech-study-diario/` — uma nota por sessão de estudo, gerada
  automaticamente (ver fluxo abaixo). É material de revisão: a matéria vem
  explicada e a nota fecha com perguntas de autoteste.
- `anotacoes-tech/` — uma nota por anotação literal (specs, decisões,
  referência), também gerada automaticamente. Aqui a IA **não** resume nem
  interpreta nada; só arruma a redação.
- `MOC Livros.md` + livros/capítulos — trilha paralela pra registrar
  leitura de livros técnicos.
- `templates/` — modelos de referência pra cada tipo de nota.
- `fotos/` — fotos que você marcou explicitamente para salvar ("salvar" no
  bruto), organizadas por data, fora do grafo do Obsidian (não versionado no git).
  Fotos lidas pro conteúdo mas não marcadas são deletadas após compilação.

## Como usar

Os dois fluxos começam do mesmo jeito. O que muda é qual skill você chama no
final — e isso decide se a IA vai **explicar** o conteúdo ou apenas
**arrumar** o que você escreveu.

### 1. Escrever o bruto

1. Copie `templates/Template nota bruta tech.md` pra um arquivo chamado
   `nota bruta tech.md` na raiz do vault. Se tiver múltiplas sessões de uma
   vez, crie também `nota bruta tech 2.md`, `nota bruta tech 3.md`, etc.
2. Preencha os 3 campos em cada arquivo: o que você está estudando
   (palavras-chave), o(s) conceito(s) envolvido(s) (em ordem de importância),
   e o estudo em si — pode ser texto solto, mal formatado, com fotos coladas,
   sem preocupação nenhuma com organização.

### 2. Escolher a skill

- **`/formatar-nota-estudo`** — pra estudo de verdade, quando você quer
  reler daqui a meses e reaprender o assunto. Reescreve e explica a matéria,
  e fecha a nota com perguntas de autoteste. Processa **todos** os brutos da
  raiz em sequência: 1º o sem número, depois o `2`, depois o `3`, etc.
  Resultado em `tech-study-diario/`.
- **`/formatar-anotacoes <arquivo>`** — pra registrar algo literal (specs,
  regras, decisões) sem a IA interpretar nada. Não resume, não corta, não
  reordena: só corrige a redação (ortografia, gíria, coesão) e quebra os
  parágrafos pra ficar legível. Processa **um** bruto por vez, o que você
  apontar. Resultado em `anotacoes-tech/`.

Nas duas, os conceitos são linkados (e criados, se você confirmar) e as
fotos marcadas com `salvar` vão pra `fotos/`. A diferença nas fotos: na de
estudo, toda foto vira texto na nota; na de anotação, foto marcada vira só a
imagem embedada, sem texto.

### 3. Revisar

Confira o resultado antes de seguir. O arquivo bruto é apagado
automaticamente no final — ele não serve pra mais nada depois de compilado.

## Edição segura (auto-gerado vs. manual)

Toda nota gerada — em `tech-study-diario/` ou `anotacoes-tech/` — tem
`id_obsidian` (ID único da nota) e `id_pai` (ID do conceito principal) no
frontmatter, e cada seção do corpo tem seu próprio par de marcadores
`%%--- INÍCIO AUTO-GERADO ---%%` / `%%--- FIM AUTO-GERADO ---%%` (comentário
do Obsidian, desaparece no modo leitura).
Só o miolo entre esses marcadores é gerado/regravado pela IA; qualquer coisa
que você escrever fora deles — mesmo dentro da mesma seção — fica intocada.
A seção `## ✍️ Notas minhas`, no fim de toda nota, é espaço livre seu e nunca
é preenchida pela IA.
Conceitos também têm `id_obsidian`, pra permitir referenciar uma nota
específica sem depender de busca por título.

## Próximos passos

- Skill que compile, por conceito, todas as sessões de `tech-study-diario/`
  que citam esse `[[Conceito]]` num único documento — pra jogar a pasta
  compilada inteira no NotebookLM e ter o contexto completo de estudo sobre
  aquele tema.
- "Ver um modo de mudar a skill para que caso o nome do tech study diario seja o mesmo ou o texto seja parecido e ele procura isso caso o conceito ja exista entao ele somente edita e aumenta o texto, nao cria um novo"

## Adaptando pro seu próprio vault

As skills (`.claude/skills/formatar-nota-estudo/` e
`.claude/skills/formatar-anotacoes/`) dependem da estrutura de templates já
existente neste vault. Pra usar isso no seu próprio vault, ajuste primeiro os
templates em `templates/` e depois as regras em `reference/*.md` de cada
skill pra bater com o que você mudou.
