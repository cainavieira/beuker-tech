# Regras de organização das fotos

## As duas funções de uma foto

Toda foto colada no bruto é **material de estudo**, não anexo. Ela existe
para ser lida e virar texto. Além disso, uma parte delas — só as que o
usuário marcar explicitamente — também fica embedada na nota final.

1. **Sempre**: leia o conteúdo da imagem (abra o arquivo, não deduza pelo
   nome) e use o que está nela para escrever as seções da nota tech-study,
   principalmente 📖 "Conteúdo" — é matéria como qualquer outra, e muitas
   vezes a foto é a **única** fonte do detalhe (a sintaxe exata do slide, a
   mensagem de erro do print). Print de terminal, slide, diagrama, trecho de
   código, anotação à mão: tudo entra no resumo como texto reescrito, igual a
   qualquer outra parte do bruto. Print de erro alimenta 🐞 "Erros e como
   resolvi".
2. **Só quando marcada**: além de virar texto, a foto é embedada na nota com
   link markdown (ver abaixo). Foto não marcada é arquivada em `fotos/` sem
   nenhum link — o aprendizado dela sobrevive no texto, a imagem em si sai do
   grafo do Obsidian de propósito.

Nunca ignore uma foto por ela não estar marcada para salvar: a marcação
decide se ela vira link, não se ela vira conteúdo.

## Localização de origem

- O vault não tem pasta de anexos configurada no Obsidian, então imagens
  coladas/embedadas no bruto ficam na mesma pasta do arquivo bruto (raiz do
  vault). Procure ali os arquivos referenciados (`![[...]]` ou `![](...)`)
  pelo nome citado no bruto.

## Renomeação e destino

- Toda foto referenciada vai para `fotos/` (raiz do vault, já existe — não
  criar de novo), marcada ou não.
- Nome novo: `foto yyyy-mm-dd hh-mm-ss.<extensão original>`, usando a
  data/hora de criação/modificação do próprio arquivo de imagem (não a data
  da sessão de estudo).
- Se duas fotos caírem no mesmo segundo, acrescente sufixo `-2`, `-3`... ao
  nome.

## Como o usuário marca uma foto para salvar

- A marcação vem **na linha (ou linhas) imediatamente abaixo** da referência
  da foto no bruto, escrita pelo usuário. A palavra canônica é `salvar`, mas
  aceite qualquer instrução explícita equivalente ("salvar essa", "manter
  essa foto", "salva essa aqui na nota").
- Se o usuário escrever `salvar: <texto>`, o `<texto>` é a legenda da foto e
  vira o alt do link markdown. Sem legenda, o alt é o nome novo do arquivo
  sem extensão.
- A marcação vale só para a foto imediatamente acima dela — nunca propague
  para as outras fotos do bruto.
- **Nunca embede uma foto por conta própria.** Sem marcação explícita, não
  embede, mesmo que a imagem pareça central para a sessão. Se a linha abaixo
  da foto for ambígua (parece comentário sobre o conteúdo, não pedido de
  salvar), **pare e pergunte** antes de decidir.

## Como embedar a foto marcada

- Sintaxe markdown padrão, sempre com o caminho relativo à raiz do vault e
  entre `< >` (o nome do arquivo tem espaços; sem os sinais o link quebra):

  ```markdown
  ![foto 2026-07-26 14-32-08](<fotos/foto 2026-07-26 14-32-08.png>)
  ```

  Com legenda:

  ```markdown
  ![print do erro de permissão no docker run](<fotos/foto 2026-07-26 14-32-08.png>)
  ```

- Não use `![[wikilink]]` para foto — o embed de foto é sempre a sintaxe
  `![alt](<caminho>)`.
- O caminho aponta para o nome **novo** do arquivo, já em `fotos/`, depois de
  mover e renomear. Nunca linke o nome original do bruto.
- **Onde colocar**: dentro do par de marcadores
  `%%--- INÍCIO AUTO-GERADO ---%%` / `%%--- FIM AUTO-GERADO ---%%` da seção
  que fala daquele assunto, logo abaixo do bullet ou parágrafo que a foto
  ilustra
  (normalmente 📖 "Conteúdo"; print de erro vai em 🐞 "Erros e como resolvi").
  Nunca fora dos marcadores, nunca na seção `## ✍️ Notas minhas`, e nunca em
  ❓ "Autoteste" — imagem ali entrega a resposta antes da pergunta.
- Embed não substitui texto: o trecho acompanhado da foto continua explicando
  em palavras o que a imagem mostra.
