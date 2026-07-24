# Study Tech Pessoal — contexto do vault

Vault pessoal do Obsidian pra acompanhar estudos de tecnologia. Este arquivo
existe pra qualquer sessão futura do Claude Code entender a estrutura sem
precisar redescobrir tudo do zero.

## Hierarquia principal

```
Objetivos Tech Pessoal.md    (norte, objetivos de longo prazo)
  └─ moc areas/<Área>.md      (ex.: DevOps, IA — só linka conceitos, sem conteúdo)
       └─ conceitos/<Conceito>.md   (evergreen, ex.: "Claude", "Azure DevOps")
            └─ tech-study-diario/<sessão>.md   (1 arquivo por sessão de estudo)
```

Existe uma segunda hierarquia paralela, pra livros:

```
MOC Livros.md
  └─ livro (template: Template livro.md)
       └─ capítulo (template: Template capítulo.md)
```

## Regras de conteúdo (importantes, não óbvias)

- **`moc areas/*.md`**: só listas de `[[Conceito]]`, nunca conteúdo de
  estudo. Não decidir sozinho quando um conceito "já domina" o suficiente
  pra ir em "Conceitos dominados / revisão" — julgamento de maturidade é do
  usuário.
- **`conceitos/*.md`**: as seções "O que é isso", "Por que estou estudando",
  "Recursos", "Notas soltas/dúvidas" são processamento pessoal do usuário,
  escritas com as próprias palavras dele. **Nunca escrever nelas
  automaticamente** — só criar o esqueleto vazio, e só com confirmação
  explícita. Todo conceito tem `id_obsidian` (frontmatter, formato
  `YYYYMMDD-HHMMSS` da criação do arquivo) — serve pra outras notas
  referenciarem esse conceito exatamente por ID, sem depender de match por
  tema.
- **`tech-study-diario/*.md`**: cada sessão de estudo gerada pela skill
  `formatar-nota-estudo` (ver abaixo) é sempre um arquivo novo, nunca edição
  de uma sessão anterior. Toda nota tem `id_obsidian` (ID próprio da sessão)
  e `id_pai` (o `id_obsidian` do conceito principal) no frontmatter, formato
  `YYYYMMDD-HHMMSS`. **Cada seção** (📚, 💡, 🧠, 🔗, 🔁, 🗒️) tem seu próprio
  par de marcadores `--- INÍCIO AUTO-GERADO ---` / `--- FIM AUTO-GERADO ---`
  — não é um bloco único pra nota inteira. Só o miolo entre esse par, dentro
  de cada seção, pode ser escrito/sobrescrito pela skill; qualquer coisa que
  o usuário escrever fora dos marcadores, mesmo dentro da mesma seção (ex.:
  logo abaixo do FIM), fica intocada. A seção `## ✍️ Notas minhas`, sem
  marcadores, é espaço livre genérico. Se o usuário pedir pra editar uma nota
  tech-study já existente, encontre-a pelo `id_obsidian` informado (nunca por
  busca/match de título) e só altere conteúdo dentro do par de marcadores da
  seção certa.
- **`templates/*.md`**: só referência de estrutura (frontmatter + seções).
  Nunca preencher um template com placeholders e deixar assim — o arquivo
  final não pode conter `{{}}`.
- **`fotos/`**: fotos citadas nas notas brutas, renomeadas
  `foto yyyy-mm-dd hh-mm-ss.ext` pela data do próprio arquivo de imagem.
  Pasta gitignored (não vale a pena versionar). **Nunca linkadas/embedadas
  em nenhuma nota** — organização física pura, fora do grafo do Obsidian de
  propósito.

## O fluxo de captura de estudo

1. Durante/depois de estudar, o usuário escreve tudo bruto (texto
   malformado, fotos) em `nota bruta tech.md` na raiz do vault (nome fixo,
   case-insensitive, um arquivo por vez — a partir de
   `templates/Template nota bruta tech.md`).
2. A skill `formatar-nota-estudo` (`.claude/skills/formatar-nota-estudo/`)
   compila isso numa nota `tech-study-diario/` formatada, linka/cria
   conceitos, organiza fotos, e apaga o bruto ao final. O SKILL.md e os
   arquivos em `reference/` já cobrem as regras de match/criação de
   conceito, tom de resumo e fotos — não duplicar essas regras aqui.
3. A ideia central: durante a aula/estudo o usuário só presta atenção e
   despeja informação crua — a formatação bonita fica por conta da skill,
   não do usuário no calor da hora.

## Princípios gerais ao editar este vault

- Nunca decidir estrutura (criar conceito novo, vincular a uma área) sem
  perguntar antes — mesmo quando a resposta parece óbvia.
- Nunca commitar automaticamente. Commit é sempre decisão manual do
  usuário.
- Manter os templates existentes como única fonte de verdade de
  frontmatter/seções — se um template mudar, as regras que dependem dele
  (na skill) precisam ser atualizadas junto.
- Os marcadores `--- INÍCIO/FIM AUTO-GERADO ---` são convenção lida por
  instrução, não uma trava técnica — nada no Obsidian ou no filesystem
  impede escrever fora deles por engano. A garantia real contra dano é o
  controle de versão: o vault é um repo git, então toda edição fica visível
  em `git diff` antes de qualquer commit, e nada é irreversível.
