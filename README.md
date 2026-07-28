# Study Tech Pessoal

Vault de Obsidian pra organizar anotações de estudo de tecnologia, com uma
skill de [Claude Code](https://claude.com/claude-code) que transforma
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
  automaticamente (ver fluxo abaixo).
- `MOC Livros.md` + livros/capítulos — trilha paralela pra registrar
  leitura de livros técnicos.
- `templates/` — modelos de referência pra cada tipo de nota.
- `fotos/` — fotos organizadas por data, fora do grafo do Obsidian (não
  versionado no git).

## Como usar

1. Copie `templates/Template nota bruta tech.md` pra um arquivo chamado
   `nota bruta tech.md` na raiz do vault.
2. Preencha os 3 campos: o que você está estudando (palavras-chave), o(s)
   conceito(s) envolvido(s) (em ordem de importância), e o estudo em si —
   pode ser texto solto, mal formatado, com fotos coladas, sem
   preocupação nenhuma com organização.
3. Peça pro Claude Code formatar (ele detecta e chama a skill sozinho, ou
   digite `/formatar-nota-estudo`).
4. Revise o resultado: uma nota nova em `tech-study-diario/`, conceitos
   linkados/criados, fotos organizadas em `fotos/`. O arquivo bruto é
   apagado automaticamente no final — ele não serve pra mais nada depois
   de compilado.

## Edição segura (auto-gerado vs. manual)

Toda nota `tech-study-diario/` tem `id_obsidian` (ID único da sessão) e
`id_pai` (ID do conceito principal) no frontmatter, e cada seção do corpo
tem seu próprio par de marcadores `--- INÍCIO AUTO-GERADO --- / --- FIM
AUTO-GERADO ---`. Só o miolo entre esses marcadores é gerado/regravado pela
IA; qualquer coisa que você escrever fora deles — mesmo dentro da mesma
seção — fica intocada. Conceitos também têm `id_obsidian`, pra permitir
referenciar uma nota específica sem depender de busca por título.

## Próximos passos

- Skill que compile, por conceito, todas as sessões de `tech-study-diario/`
  que citam esse `[[Conceito]]` num único documento — pra jogar a pasta
  compilada inteira no NotebookLM e ter o contexto completo de estudo sobre
  aquele tema.
- "Ver um modo de mudar a skill para que caso o nome do tech study diario seja o mesmo ou o texto seja parecido e ele procura isso caso o conceito ja exista entao ele somente edita e aumenta o texto, nao cria um novo"

## Adaptando pro seu próprio vault

A skill (`.claude/skills/formatar-nota-estudo/`) depende da estrutura de
templates já existente neste vault. Pra usar isso no seu próprio vault,
ajuste primeiro os templates em `templates/` e depois as regras em
`reference/*.md` da skill pra bater com o que você mudou.
