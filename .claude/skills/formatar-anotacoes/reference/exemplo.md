# Exemplo de referência: bruto → nota de anotação

Um par completo de entrada e saída, para calibrar o **nível de intervenção**
esperado — que é bem menor que o de `formatar-nota-estudo` no conteúdo, mas
não é zero na redação.

## Como usar este arquivo

- **Regra ganha do exemplo.** Se algo aqui contradisser um `reference/*.md`,
  a regra vale e o exemplo está desatualizado — corrija o exemplo.
- **Nunca copie conteúdo daqui para uma nota real.** O assunto é Docker por
  acaso; se a anotação real também for de Docker, escreva do bruto do
  usuário, não daqui. O que se imita é o nível de correção, nunca a matéria.
- Este arquivo **não** é uma nota do vault: mora em `.claude/`, que o
  Obsidian não indexa. Não o mova para `anotacoes-tech/`, não o linke em
  nenhuma nota. O ID e as imagens abaixo são fictícios.
- Se o template `templates/template-tech-notes.md` mudar, atualize este
  exemplo junto.

---

## Entrada: `nota bruta tech.md`

```markdown
# Nota bruta

## O que estou estudando
comandos docker basicos e diferenca de imagem/container

## Conceito (ordem de importância)
- Docker

## Estudo
- docker pull baixa a imagem do registry, se n especificar tag vem latest
- docker images lista as imagens que ja tem local
- docker ps só mostra o que ta rodando, com -a aparece os parado tb

mano entao aquele nego de imagem e container, saquei um pouco mais hj, tipo
a imagem é a receita e o container é o prato pronto, dai vc pode fazer
varios prato da mesma receita e eles nao se misturam, sla, e daí o exec
serve pra vc entrar dentro do container que ja tá rodando, roda ele com -it
que nem terminal mesmo, entendeu, e se o container tiver parado da erro pq
n tem processo rodando ali dentro pra "entrar"

![[Pasted image 20260810093211.png]]
salvar

![[Pasted image 20260810093504.png]]
```

Repare: o parágrafo corrido depois dos bullets é uma "parede de texto" —
várias ideias diferentes (receita/prato, `exec`, erro no container parado)
grudadas sem parágrafo nenhum, cheia de gíria e vício de linguagem ("sla",
"entendeu", "tipo"). E há duas fotos: a primeira marcada com `salvar`, a
segunda sem marcação nenhuma.

## Saída: `anotacoes-tech/Comandos Docker básicos.md`

Título proposto a partir do campo livre e confirmado com o usuário antes de
criar o arquivo (`titulos.md`).

```markdown
---
tipo: tech-notes
data: 2026-08-10
tags:
  - tech-notes
conceito: ["[[Docker]]"]
id_obsidian: 20260810-093740
id_pai: 20260724-110454
---

# 📅 Comandos Docker básicos

## 📝 Conteúdo

%%--- INÍCIO AUTO-GERADO ---%%
- `docker pull` baixa a imagem do registry, se não especificar tag vem
  `latest`.
- `docker images` lista as imagens que já tem local.
- `docker ps` só mostra o que está rodando, com `-a` aparecem os parados
  também.

Entendi um pouco melhor a diferença entre imagem e container hoje. A imagem
é a receita, e o container é o prato pronto — dá para fazer vários pratos a
partir da mesma receita, sem que eles se misturem entre si.

O `exec` serve para entrar dentro de um container que já está em execução,
rodando com `-it` como se fosse um terminal. Se o container estiver parado,
dá erro, porque não há processo rodando ali dentro para "entrar".

![tabela de comandos básicos do Docker](fotos/foto-2026-08-10-09-32-11.png)

O diagrama mostra uma imagem única no topo, com três setas saindo dela para
três containers diferentes embaixo — reforçando que vários containers
independentes nascem da mesma imagem, sem se afetarem entre si.
%%--- FIM AUTO-GERADO ---%%

## ✍️ Notas minhas

-
```

## O que este exemplo demonstra

- **Comandos: só correção objetiva.** Os três primeiros bullets já estavam
  bem formados no bruto — só ortografia e pontuação mudaram ("se n
  especificar" → "se não especificar"). Nada foi reescrito além disso
  porque não havia nada de subjetivo para corrigir ali.
- **Prosa: correção subjetiva de verdade.** O parágrafo corrido virou texto
  limpo — gíria e vício de linguagem fora ("mano", "sla", "tipo",
  "entendeu"), frase corrida virou frase bem construída, conectivos
  entraram onde faltava coesão. Mas **nenhuma ideia nova entrou e nenhuma
  saiu**: receita/prato, `exec`, e o erro no container parado são
  exatamente as três ideias do bruto, na mesma ordem, com o mesmo nível de
  detalhe — só a redação melhorou.
- **Parágrafos quebrados, não conteúdo cortado.** A parede de texto do
  bruto virou dois parágrafos (receita/prato num, `exec`/erro no outro)
  porque o próprio bruto já mudava de assunto ali — a skill só inseriu a
  quebra que faltava. Isso **não** é a mesma coisa que resumir: o texto
  final tem o mesmo conteúdo, só mais fácil de reler.
- **Foto marcada não vira texto.** A primeira foto (`salvar`) foi só
  movida, renomeada e embedada — nenhuma frase do "📝 Conteúdo" descreve o
  que está nela. O embed sozinho é a "anotação" daquela foto.
- **Mas o `alt` dela é descritivo**, não o nome do arquivo. Como o usuário
  escreveu `salvar` sem legenda, a imagem foi aberta só para gerar "tabela
  de comandos básicos do Docker" — e o resultado dessa leitura foi
  **exclusivamente** para o `alt`, sem virar frase no corpo.
- **Foto não marcada foi explicada, não só transcrita.** A segunda foto
  não tinha marcação, então foi deletada da raiz depois da compilação — e
  como não sobra em lugar nenhum, o parágrafo final não descreve palavra
  por palavra o que está escrito na imagem, ele **explica o que o diagrama
  representa** (a relação um-para-muitos entre imagem e containers), do
  jeito que `formatar-nota-estudo` trataria essa mesma foto. Isso é a única
  exceção ao "nunca explicar" da skill.
- **Nenhuma seção extra.** Não existe 💡 Insight, 🐞 Erro isolado, 🧠 Dúvida
  nem ❓ Autoteste — só "📝 Conteúdo", porque decidir o que é "insight" ou
  "dúvida" já seria inferência, e isso a skill não faz.
- **✍️ vazia**, sempre.
