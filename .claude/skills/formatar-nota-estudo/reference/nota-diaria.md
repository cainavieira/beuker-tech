# Regras de compilação da nota tech-study

O objetivo da nota não é registrar que a sessão aconteceu — é ser **material
de revisão**: alguém (o próprio usuário, meses depois) precisa reaprender o
assunto lendo só essa nota, sem lembrar da sessão e sem voltar à fonte.
Toda regra abaixo existe por causa disso.

## Frontmatter

- `tipo: tech-study`
- `data:` — data real da sessão (hoje, a menos que o bruto deixe claro outra
  data).
- `tags: [tech-study]`
- `conceito:` — **lista** com os wikilinks de **todos** os conceitos tocados na
  sessão, o principal primeiro, na mesma ordem em que o usuário escreveu no
  bruto: `conceito: ["[[Docker]]", "[[Linux]]"]`. Com um conceito só, ainda é
  lista: `conceito: ["[[Docker]]"]`. É lista para que uma sessão seja
  encontrável por qualquer conceito que ela tocou, não só pelo principal — mas
  a primeira posição continua sendo o que define o principal (e é dela que sai
  o `id_pai`).

Não existe campo de disciplina, aula, semestre ou avaliação, de propósito: a
origem do aprendizado (faculdade, curso, conta própria) é irrelevante para a
nota — o que importa é o que foi aprendido. Não invente esses campos nem
mencione a origem no corpo, a menos que o usuário escreva isso no bruto.

## Corpo — as seções

**Nunca copie o bruto cru.** Anotação solta e mal formatada do bruto vira
texto coeso nas seções certas.

### Melhorar sim, inventar não

Reescrever para ficar mais claro é o trabalho principal da skill, e às vezes
isso significa acrescentar algo que o bruto não disse com todas as letras. A
fronteira não é "acrescentou ou não" — é **se o acréscimo continua dentro do
que a sessão cobriu**.

Melhoria legítima, faça sem medo:

- Deixar mais clara uma explicação que o bruto deu de forma confusa ou pela
  metade.
- Corrigir erro factual do bruto (nome de comando trocado, sintaxe errada,
  termo usado fora do lugar). Quando o erro for do tipo que o usuário pode
  repetir, vale registrar a correção em 📖 em vez de apagá-la em silêncio.
- Tornar explícita uma conexão que ficou implícita entre duas coisas que o
  próprio bruto citou.
- Completar a sintaxe de um comando citado pela metade, quando o bruto ou a
  foto mostram qual é.
- Organizar melhor: agrupar o que está espalhado, dar subtítulo, escolher
  entre prosa e lista conforme a regra abaixo.

Invenção, nunca:

- Puxar tópico, comando ou conceito que a sessão não tocou, mesmo sendo o
  "próximo assunto natural" ou algo que combinaria bem ali.
- Encher seção rasa com definição genérica de documentação só para ela não
  ficar curta. Seção curta é resposta honesta a bruto curto.
- Afirmar detalhe que não está no bruto nem na foto (versão, flag, valor
  padrão, comportamento em caso de erro), ainda que você saiba que é verdade.

**O teste é sempre o mesmo: a nota mente sobre o que o usuário estudou?** Se
o acréscimo faz ele reler daqui a três meses e concluir que aprendeu algo que
nunca viu na sessão, está errado — mesmo estando factualmente correto. Na
dúvida, o lugar da lacuna é 🧠 "Dúvidas / pontos a aprofundar", não uma frase
inventada em 📖.

### Links sobrevivem sempre intactos

Única exceção rígida à regra acima. Qualquer link colado no bruto — URL
solta (`https://...`), markdown (`[texto](url)`), referência a vídeo/doc/
repositório com URL junto — nunca é reescrito, parafraseado, encurtado,
"limpo" (removendo query string, `www.`, barra final etc.) ou dropado
durante a reescrita da prosa ao redor. Copie a URL caractere por caractere,
exatamente como está no bruto, não importa em qual seção ela acabe (📖, 🔗,
💡, onde for) nem se está embutida no meio de um parágrafo que vai ser
resumido — extraia e preserve o link, resuma só o texto ao redor dele. Se
não estiver claro se um trecho colado é uma URL válida ou só texto parecido
com uma, trate como link e preserve.

### Bullet e parágrafo são os dois formatos válidos

Isto é um resumo pessoal escrito pelo usuário, não um relatório: **parágrafo
em prosa é formato de primeira classe**, tanto no bruto quanto na nota final.
Não converta tudo em lista por reflexo — bullet picado é ruim justamente para
o que mais importa (explicar, conectar ideias, raciocinar), porque quebra o
encadeamento entre as frases.

Escolha pelo conteúdo:

- **Prosa** quando é explicação, raciocínio, comparação entre duas coisas ou
  narrativa do que aconteceu. Dois ou três parágrafos curtos numa seção é
  perfeitamente normal.
- **Lista** quando os itens são realmente enumeráveis e independentes:
  comandos, flags, passos de um procedimento, itens que o usuário vai varrer
  com o olho.
- **Misturado**, que é o caso mais comum numa seção boa: um parágrafo
  situando o assunto, e a lista logo abaixo com os itens concretos.

E respeite o registro do usuário: se ele escreveu em prosa no bruto, não
fatie o texto dele em bullets; se escreveu em tópicos soltos, não infle em
parágrafos artificiais. Reescrever para ficar claro é o trabalho — trocar a
forma de expressão dele sem motivo, não.

As duas exceções em que o formato é fixo (e por um motivo funcional, não
estético): 📚 é sempre uma linha por conceito, porque é índice; 🧠 e 🔁 são
sempre checkbox, porque precisam ser varridos por busca entre as notas.

- **📚 O que estudei hoje** — só o **escopo** da sessão, 1 linha por conceito
  tocado, no formato `[[Conceito]] — o que foi feito`. É índice, não conteúdo:
  a matéria em si vai em 📖. Sem sintaxe, sem explicação, sem lista de
  comandos aqui.
- **📖 Conteúdo** — a matéria de verdade, e a seção mais importante da nota.
  Cada item aprendido (comando, conceito, sintaxe, regra, definição) ganha:
  o que é, como se usa/sintaxe, e quando serve. Formato livre conforme a regra
  acima: conceito que precisa ser entendido pede prosa (um parágrafo
  explicando imagem vs. container ensina mais que dois bullets justapostos),
  conjunto de comandos ou flags pede lista, e a seção pode ter os dois. Use
  subtítulo `###` se a sessão cobriu assuntos bem distintos. Comando ou código
  sempre em `backtick` ou bloco de código com a linguagem.
  O nível esperado está demonstrado em `exemplo.md` — consulte antes de
  escrever esta seção.
  Se o bruto foi raso demais para isso (só citou o nome do comando), escreva
  o que dá para escrever com honestidade e registre a lacuna em 🧠 — nunca
  preencha com definição inventada ou genérica.
- **💡 Aprendizados / insights** — **só** o que era novo ou contraintuitivo
  para o usuário: uma conexão nova, uma intuição que faltava, um "ah, então é
  por isso que...". Definição, descrição e resumo do que foi visto **não**
  entram aqui — o lugar deles é 📖. Se o candidato a insight puder ser lido
  numa doc qualquer, não é insight: corte. Prosa costuma cair melhor aqui:
  insight é raciocínio, e raciocínio encadeado não sobrevive picado em bullet.
- **🐞 Erros e como resolvi** — o que quebrou durante a prática: a mensagem de
  erro (ou o sintoma), a causa real, e a correção — nessa ordem, em lista ou
  em prosa (erro cuja causa exige explicação fica melhor em parágrafo). Só o
  que de fato aconteceu no bruto; nunca antecipe erro hipotético.
- **🧠 Dúvidas / pontos a aprofundar** — dúvidas reais que apareceram no
  bruto, como checkbox `- [ ]` e com destino explícito quando o bruto
  indicar (`- [ ] perguntar pro professor: ...`, `- [ ] procurar na doc:
  ...`). Checkbox porque uma busca por `- [ ]` em `tech-study-diario/` vira a
  lista de pendências de estudo. Se a dúvida precisar de contexto para fazer
  sentido depois, a linha do checkbox fica curta e o parágrafo explicando vem
  indentado embaixo dela — o checkbox é obrigatório, a concisão não. Nunca
  invente dúvida nem deixe genérico tipo "revisar depois" sem contexto.
- **🔗 Recursos usados** — as fontes citadas no bruto, do jeito que o usuário
  citou: link, nome do vídeo, doc, livro, repositório. Nada além disso —
  **não** exija nem pergunte página, capítulo, número de slide ou timestamp;
  o usuário não anota esse nível de detalhe e cobrar isso só atrapalha a
  captura. Se ele escrever a localização por conta própria, preserve; se não,
  a fonte sozinha basta. Se o link vier junto, aplica a regra de "Links
  sobrevivem sempre intactos" acima — copiado exato, nunca alterado. Se o
  bruto não citou fonte nenhuma, a seção é omitida (é opcional).
- **🔁 Próximos passos** — checkbox `- [ ]`, mesma razão de 🧠. Só se o bruto
  indicar algo concreto; não invente próximo passo.
- **❓ Autoteste** — 3 a 5 perguntas de recuperação ativa geradas a partir de
  📖, cada uma num callout dobrável do Obsidian (resposta escondida por
  padrão, o `-` depois de `[!question]` é o que colapsa):

  ```markdown
  > [!question]- O que `docker exec -it` faz e por que o `-it` importa?
  > Abre uma sessão interativa num container já em execução. `-i` mantém o
  > stdin aberto e `-t` aloca um pseudo-terminal; sem os dois não há shell
  > utilizável.
  ```

  Regras: pergunta que exige lembrar ou explicar ("por que", "qual a
  diferença entre", "o que acontece se"), nunca pergunta de sim/não nem que
  se responde copiando uma palavra do título. A resposta é escrita em prosa,
  como você explicaria em voz alta. A resposta sai **só** do que
  está em 📖 na própria nota — nunca de conhecimento externo que o usuário
  não estudou nessa sessão. Se 📖 tiver conteúdo para menos de 3 perguntas
  boas, faça menos; não encha.
- **✍️ Notas minhas** — sempre presente, sempre vazia, nunca preenchida pela
  skill.

## Seções vazias

- Ordem canônica das seções: 📚, 📖, 💡, 🐞, 🧠, 🔗, 🔁, ❓, ✍️.
- **Núcleo fixo, sempre presente**: 📚, 📖, ❓ e ✍️.
- As opcionais (💡, 🐞, 🧠, 🔗, 🔁) só entram na nota **se tiverem conteúdo
  real**. Sem conteúdo, omita a seção inteira — título e marcadores — em vez
  de deixar bullet vazio. Nota que é metade andaime não serve para revisar.
- Se uma edição futura precisar acrescentar uma seção antes omitida, insira-a
  na posição da ordem canônica acima, já com o par de marcadores.

## Identificação (id_obsidian / id_pai)

- Toda nota tech-study recebe `id_obsidian`, gerado no momento da criação da
  nota, formato `YYYYMMDD-HHMMSS` (data e hora local de criação, até o
  segundo — necessário porque a skill costuma criar conceito(s) e a nota
  tech-study quase no mesmo instante, e colisão por minuto é comum). Se por
  acaso colidir com um `id_obsidian` já existente (duas notas no mesmo
  segundo), acrescente sufixo `-2`, `-3`...
- `id_pai` recebe o `id_obsidian` já existente no frontmatter do conceito
  principal (o primeiro item da lista `conceito:`, que é o primeiro do
  bruto). **Nunca infira ou gere esse ID por conta própria** — ele sempre
  vem do arquivo de conceito já resolvido pelo processo de match/criação de
  `reference/conceitos.md`; o conceito em si é sempre o que o usuário
  escreveu no bruto, nunca inferido do texto livre.

## Zona auto-gerada

- Cada seção tem seu **próprio** par de marcadores
  `%%--- INÍCIO AUTO-GERADO ---%%` / `%%--- FIM AUTO-GERADO ---%%` — não é um
  bloco único cobrindo a nota inteira. A skill só escreve dentro desses
  marcadores, título da seção (`##`) sempre fora.
- Os marcadores vão sempre entre `%% %%`: é comentário do Obsidian, então
  desaparecem no modo leitura (a nota fica limpa para estudar) e continuam
  visíveis no modo source, para a skill e para o usuário. Nunca escreva o
  marcador sem os `%%`.
- Isso deixa espaço pro usuário escrever manualmente dentro da mesma seção,
  fora do par de marcadores dela (ex.: acrescentar uma linha própria embaixo
  do `%%--- FIM AUTO-GERADO ---%%` de "💡 Aprendizados / insights", ainda
  dentro dessa seção). Esse conteúdo nunca deve ser tocado.
- Ao gerar a nota pela primeira vez, preencha só o miolo de cada bloco (entre
  os marcadores daquela seção), mantendo os marcadores intactos.
- A nota final **não** leva nenhum texto explicando os marcadores: instrução
  de ferramenta não entra em material de estudo. A explicação vive só no
  template e neste arquivo.
- A seção `## ✍️ Notas minhas`, no fim do arquivo e sem marcadores, é criada
  vazia e nunca preenchida pela skill — espaço livre genérico, fora de
  qualquer seção específica.
- Se o usuário pedir uma edição numa nota tech-study já existente (apontando
  pelo `id_obsidian`), localize a seção certa e só altere o conteúdo entre o
  par de marcadores **daquela seção**; tudo fora de marcadores, em qualquer
  seção, fica intocado.

## Nome e local do arquivo

- O nome do arquivo é o **título derivado e confirmado** a partir da seção "O
  que estou estudando" do bruto — nunca o texto cru dela. Regras de derivação,
  confirmação com o usuário e histórico de estilo: ver `reference/titulos.md`.
- `tech-study-diario/<título confirmado>.md` (ex.:
  `tech-study-diario/Debug de skills do Claude Code.md`).
- Se já existir um arquivo com esse nome (duas sessões com o mesmo título),
  acrescente a data da sessão entre parênteses —
  `Comandos Docker (2026-07-24).md` — em vez de sufixo `-2`, `-3`: o nome
  precisa distinguir as sessões para o usuário, e um número não distingue
  nada. Se ainda colidir (duas sessões do mesmo tema no mesmo dia), aí sim
  acrescente `-2` depois da data. **Nunca sobrescreva uma sessão anterior.**
