# Regras de organização das fotos

## Os dois caminhos de uma foto

A marcação do usuário decide o destino da foto, e os caminhos são
**exclusivos** — nunca os dois ao mesmo tempo:

1. **Marcada para salvar**: vai para `fotos/`, é renomeada e embedada na
   nota. **Não gera texto nenhum** — nem transcrição, nem explicação. A
   imagem já fica guardada e visível na nota; reescrever em palavras o que
   ela mostra é redundante.
2. **Não marcada**: é **deletada** após a compilação, não sobra em lugar
   nenhum. Por isso o conteúdo dela precisa virar texto em "📝 Conteúdo", e
   precisa ser **explicado**, não só transcrito (ver a última seção).

Isso é o inverso de `formatar-nota-estudo`, onde toda foto vira texto e a
marcação decide só se ela é guardada. Aqui a marcação decide as duas coisas.

## Quando abrir a imagem

Abrir imagem custa tempo — abra só quando o resultado vai ser usado:

- **Foto não marcada**: sempre abra. É a única fonte do conteúdo dela, que
  vai virar texto.
- **Foto marcada, com legenda** (`salvar: <legenda>`): não abra. A legenda
  do usuário já é o `alt`, e nada mais dela vai para a nota.
- **Foto marcada, sem legenda**: abra rapidamente, só para escrever um `alt`
  descritivo (ver abaixo). O resultado dessa leitura vai **exclusivamente**
  para o `alt` — nunca vira frase no corpo da nota.

## Localização de origem

O vault não tem pasta de anexos configurada no Obsidian, então imagens
coladas/embedadas no bruto ficam na mesma pasta do arquivo bruto (raiz do
vault). Procure ali os arquivos referenciados (`![[...]]` ou `![](...)`)
pelo nome citado no bruto.

## Renomeação e destino

- **Só as fotos marcadas** vão para `fotos/` (já existe — não criar de
  novo). Fotos não marcadas são deletadas.
- Nome novo: `foto-yyyy-mm-dd-hh-mm-ss.<extensão original>`, usando a
  data/hora de criação/modificação do próprio arquivo de imagem (não a data
  da anotação). **Tudo ligado por traço, sem espaço nenhum** — espaço no
  nome quebra o link markdown quando falta envolver o caminho em `< >`, e
  ligar por traço elimina essa classe de erro de uma vez.
- Se duas fotos caírem no mesmo segundo, acrescente sufixo `-2`, `-3`... ao
  nome.

## Como o usuário marca uma foto para salvar

- A marcação vem **na linha (ou linhas) imediatamente abaixo** da referência
  da foto no bruto. A palavra canônica é `salvar`, mas aceite qualquer
  instrução explícita equivalente ("salvar essa", "manter essa foto", "salva
  essa aqui na nota").
- A marcação vale só para a foto imediatamente acima dela — nunca propague
  para as outras fotos do bruto.
- **Nunca embede uma foto por conta própria.** Sem marcação explícita, não
  embede, mesmo que a imagem pareça central. Se a linha abaixo da foto for
  ambígua (parece comentário sobre o conteúdo, não pedido de salvar),
  **pare e pergunte** antes de decidir.

## Como embedar a foto marcada

Sintaxe markdown padrão, caminho relativo à raiz do vault. Como o nome novo
não tem espaço, o link funciona sem precisar de `< >` ao redor do caminho:

```markdown
![diagrama de imagem gerando três containers](fotos/foto-2026-07-26-14-32-08.png)
```

- **O `alt` nunca é o nome do arquivo.** `![foto-2026-07-26-14-32-08](...)`
  não diz nada a quem relê a nota nem à busca do Obsidian. O `alt` sai, nesta
  ordem: a legenda do usuário (`salvar: <legenda>`), se houver; senão, uma
  descrição curta (3 a 8 palavras) do que a foto mostra, tirada do contexto
  do bruto ao redor dela ou de uma olhada rápida na imagem.
- Não use `![[wikilink]]` para foto — o embed de foto é sempre a sintaxe
  `![alt](caminho)`.
- O caminho aponta para o nome **novo** do arquivo, já em `fotos/`, depois de
  mover e renomear. Nunca linke o nome original do bruto.
- **Onde colocar**: dentro do par de marcadores
  `%%--- INÍCIO AUTO-GERADO ---%%` / `%%--- FIM AUTO-GERADO ---%%` da seção
  única "📝 Conteúdo", no ponto do texto correspondente ao lugar onde a foto
  apareceu no bruto (mesmo sem haver texto sobre ela ali — é só o embed).
  Nunca fora dos marcadores, e nunca na seção `## ✍️ Notas minhas`.

## Como explicar a foto não marcada

Esta é a única parte da skill que **explica** em vez de copiar: como a foto
não sobrevive em lugar nenhum além do texto, transcrever palavra por palavra
perderia o que ela mostra. Aqui a foto é tratada como em
`formatar-nota-estudo`.

- Entenda o que a imagem mostra, não só o texto visível nela: comando → o
  que ele faz; print de erro → o que quebrou e por quê, se der pra ver;
  slide → a ideia que ele passa; diagrama → o que ele representa, não só
  "três caixas conectadas"; anotação à mão → o conteúdo dela, reescrito de
  forma legível.
- A explicação sai **só** do que a imagem mostra, mais o contexto do resto do
  bruto — nunca de conhecimento externo. Não invente significado que a imagem
  não sustenta.
- **Se a imagem for densa demais para explicar com qualidade** (print cheio
  de texto miúdo, diagrama com muitos elementos, tabela grande), **pare e
  pergunte** ao usuário se ele prefere que ela seja salva e embedada em vez
  de explicada. A skill não pode decidir isso sozinha: salvar contraria a
  ausência de marcação no bruto, e explicar mal perde informação. Se houver
  outras perguntas pendentes na compilação, junte todas numa interação só.
