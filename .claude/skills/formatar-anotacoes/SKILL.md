---
name: formatar-anotacoes
description: Compila uma única nota bruta indicada pelo usuário (mesmo formato de "templates/Template nota bruta tech.md") numa nota de anotação em anotacoes-tech/, no padrão de "templates/template-tech-notes.md". Diferente da formatar-nota-estudo, é literal no conteúdo (nunca resume, corta, adiciona ou reordena ideia), mas trabalha a redação de verdade: correção de português em sentido amplo (gíria, coesão, coerência) e parágrafos quebrados para leitura fluida, direto pra seção única "Conteúdo". Ativada com /formatar-anotacoes seguido opcionalmente do caminho do bruto — sem argumento, pergunta qual arquivo usar. Use quando o usuário pedir para "formatar anotação", "compilar essa nota bruta em anotação" (não estudo), ou digitar /formatar-anotacoes.
---

# Formatar anotação (bruto → tech-notes)

Esta skill processa **uma única nota bruta**, indicada pelo usuário — nunca
escaneada automaticamente como em `formatar-nota-estudo`. Diferente da nota
tech-study, a nota gerada aqui é **literal no conteúdo**: a skill nunca
resume, corta, adiciona ou reordena uma ideia que o usuário escreveu, e
nunca completa lacuna com conhecimento externo. Se o bruto for raso, a nota
fica igualmente rasa — isso é esperado, não defeito da skill.

Mas a **redação** é trabalhada de verdade, não só o óbvio (ortografia,
concordância, pontuação): gíria, frase mal construída, falta de coesão e de
coerência viram texto bem escrito, e parede de texto vira parágrafos que se
lê sem cansar. Ver Passo 2 para a régua exata. A única exceção ao "nunca
explicar" é a foto **não marcada** para salvar (Passo 3).

## Passo 0 — Determinar qual nota bruta processar

- Se a skill foi ativada com argumento (ex.: `/formatar-anotacoes nota bruta
  tech.md` ou um caminho relativo), use esse arquivo diretamente, **sem
  perguntar**.
- Se foi ativada sem argumento (`/formatar-anotacoes` sozinho), pergunte ao
  usuário qual arquivo bruto processar antes de continuar.
- O bruto segue a mesma estrutura de `templates/Template nota bruta tech.md`
  (seções "O que estou estudando", "Conceito (ordem de importância)",
  "Estudo") — não existe um template bruto próprio para anotação, o mesmo
  arquivo-modelo serve para as duas skills.

## Passo 1 — Ler o bruto e extrair título e conceitos

- **Ignore os comentários do template.** O bruto traz instruções em blocos
  `<!-- ... -->` sob cada título, vindas de
  `templates/Template nota bruta tech.md`. São ajuda para o usuário, não
  conteúdo dele — nunca copie esse texto para a nota. Isso importa em dobro
  aqui, onde o conteúdo é copiado literalmente: o texto de ajuda cairia
  inteiro dentro de "📝 Conteúdo". O conteúdo real é o que o usuário escreveu
  **fora** dos comentários, normalmente logo abaixo, às vezes indentado
  (indentação aí é acidente de digitação, não bloco de código — não a
  preserve).
- Seção "O que estou estudando": mesma regra de derivação de título usada em
  `formatar-nota-estudo` (frase nominal curta, sentence case, sem data/emoji)
  — proponha um título e **confirme com o usuário** antes de criar o
  arquivo, e **registre o resultado na tabela de histórico de
  `reference/titulos.md`** (proposto, final, e se foi aceito sem correção).
  Esse registro não é opcional: é dele que sai o estilo das próximas
  propostas e o contador que decide quando a skill para de perguntar. O
  histórico é próprio desta skill (não compartilha o de
  `formatar-nota-estudo`, mesmo usando a mesma regra de forma).
- Seção "Conceito (ordem de importância)": mesma regra de
  `formatar-nota-estudo` — a ordem de escrita já é a prioridade, o primeiro
  item é o principal, nunca reordene. Se "Estudo" mencionar um conceito fora
  dessa lista, ou a lista estiver vazia enquanto o texto claramente fala de
  algo específico, **pare e pergunte** qual conceito usar.
- Regras completas de match/criação de conceito: ver `reference/conceitos.md`
  (idêntica à lógica de `formatar-nota-estudo`, incluindo perguntar antes de
  criar, nunca editar o conteúdo do conceito, e sugerir backlink na MOC
  area correspondente).
- **Junte as perguntas numa só interação**: se precisar confirmar título e
  também perguntar sobre conceito, pergunte as duas de uma vez.

## Passo 2 — Compilar a nota de anotação

- Gere um arquivo **novo** em `anotacoes-tech/`, seguindo a estrutura de
  `templates/template-tech-notes.md` (frontmatter + seção única "📝
  Conteúdo").
- **Copie o conteúdo da seção "Estudo" do bruto** para dentro de "📝
  Conteúdo", trabalhando a redação em sentido **amplo** — o texto final
  precisa ser agradável de reler, porque quem vai reler é o próprio usuário,
  meses depois. Isso inclui três coisas:
  - **Correção objetiva**: ortografia, concordância, pontuação,
    capitalização.
  - **Correção subjetiva**: gíria e abreviação informal ("vc", "pq", "tipo
    assim", "sla") viram forma escrita correta; frase corrida ou mal
    encadeada vira frase bem construída; falta de conectivo entre ideias
    (coesão) e frase que não fecha o raciocínio (coerência) são corrigidas.
  - **Parágrafos**: parede de texto corrido demais (várias ideias grudadas
    sem respiro) vira parágrafos menores, quebrados nos pontos onde o
    assunto ou o raciocínio já muda no bruto — pesado de ler é tão ruim
    quanto malescrito. Isso é só inserir a quebra de linha que falta onde a
    transição de ideia já existe, não reordenar nem resumir.

  A régua em tudo isso é a mesma: **o sentido, a ordem e o nível de detalhe
  não mudam nunca — só a forma como está escrito muda**. **Nunca**:
  - mude, adicione ou corte uma ideia — só a redação dela;
  - resuma, sintetize (encurtando o que foi dito) ou elabore/explique além
    do que o usuário escreveu — reescrever a frase para ficar bem escrita é
    esperado, elaborar um pensamento novo que ele não teve não é;
  - reorganize a ordem em que o usuário escreveu;
  - complete lacunas do texto do bruto com conhecimento externo ou
    explicação adicional (a foto **não marcada** do Passo 3 é a única
    exceção, e vale só para o conteúdo da imagem, nunca para o texto);
  - transforme prosa em lista nem lista em prosa — quebrar um parágrafo
    grande em parágrafos menores não é isso, continua sendo prosa, só
    respira melhor. O formato do bruto (tópicos soltos, parágrafo corrido,
    ou os dois misturados) é o formato final, só a redação e a quebra de
    parágrafo mudam.
  - **toque no interior de um link.** URL solta (`https://...`) ou markdown
    (`[texto](url)`) é copiada caractere por caractere, exatamente como está
    no bruto — a correção de português nunca entra na URL em si (nem
    acentuação, nem pontuação, nem capitalização), só no texto ao redor dela.
    Isso vale mesmo que a URL "pareça" ter erro de digitação: não é português,
    não se corrige.

  **Critério de desempate.** "Corrigir coesão" e "nunca elaborar" conflitam
  na prática: costurar duas frases soltas quase sempre exige um conectivo que
  afirma uma relação (causa, oposição, consequência) que o usuário não
  escreveu explicitamente. Quando estiver em dúvida se uma reescrita ainda é
  redação ou já virou conteúdo novo, **erre para o lado de menos
  intervenção** — texto um pouco mais tosco é melhor que texto bonito
  afirmando algo que o usuário não afirmou. Na dúvida entre dois conectivos,
  prefira o mais fraco (`e`, `daí`, ponto final separando as frases) ao mais
  forte (`portanto`, `porque`, `apesar de`): o mais forte declara uma
  relação lógica; o mais fraco só junta.
- Frontmatter — conforme `templates/template-tech-notes.md` (`tipo`, `data`,
  `tags`, `conceito`, `id_obsidian`, `id_pai`), que é a fonte de verdade da
  estrutura; os valores:
  - `tipo: tech-notes`
  - `data:` — data real da anotação (hoje, a menos que o bruto deixe claro
    outra data)
  - `tags: [tech-notes]`
  - `conceito:` — lista com os wikilinks de todos os conceitos tocados, o
    principal primeiro, na mesma ordem em que o usuário escreveu no bruto
  - `id_obsidian` — gerado no momento da criação, formato
    `YYYYMMDD-HHMMSS`; se colidir, sufixo `-2`, `-3`...
  - `id_pai` — o `id_obsidian` já existente no frontmatter do conceito
    principal. **Nunca infira ou gere esse ID por conta própria.**
- A seção `## ✍️ Notas minhas` é sempre criada vazia, nunca preenchida pela
  skill — espaço livre genérico do usuário.
- **Leia `reference/exemplo.md` antes de escrever a nota**: fixa o nível de
  redação esperado (correção ampla + parágrafos legíveis, mas conteúdo
  sempre literal — nunca ideia nova, nunca resumo).

## Passo 3 — Organizar as fotos

- A marcação do usuário (`salvar` na linha logo abaixo da foto) decide o
  destino, e os dois caminhos são exclusivos: **marcada** vira embed e não
  gera texto nenhum; **não marcada** é deletada, então precisa virar texto
  explicado — a única exceção ao "nunca explicar" desta skill.
- **Regras completas em `reference/fotos.md`** (o que ler, quando ler, como
  nomear, como embedar, como explicar). Leia esse arquivo se o bruto tiver
  ao menos uma foto; se não tiver nenhuma, pule o passo inteiro.

## Passo 4 — Mostrar o resultado e limpar

- Mostre ao usuário, na íntegra: a nota de anotação gerada, os conceitos
  criados/linkados, e a lista de fotos salvas (nome antigo → novo), marcando
  em que ponto de "📝 Conteúdo" cada uma foi embedada.
- Só depois de mostrar, limpe:
  - Apague o arquivo bruto original.
  - Delete da raiz do vault apenas as fotos **citadas neste bruto** que não
    foram marcadas para salvar — foram lidas pro conteúdo, mas não precisam
    ficar guardadas.
- **Nunca execute `git add`, `git commit` ou `git push`** como parte desta
  skill.

## Edição de nota existente

- Se o usuário pedir para editar uma nota de anotação já existente, encontre
  pelo `id_obsidian` informado (**nunca** por busca/match de título) e altere
  só o conteúdo dentro do par de marcadores
  `%%--- INÍCIO AUTO-GERADO ---%%` / `%%--- FIM AUTO-GERADO ---%%` da seção
  "📝 Conteúdo". Qualquer coisa fora dos marcadores, ou em "✍️ Notas minhas",
  fica intocada.
