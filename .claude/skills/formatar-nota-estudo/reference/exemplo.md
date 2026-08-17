# Exemplo de referência: bruto → nota tech-study

Um par completo de entrada e saída, para calibrar **nível de detalhe e tom**.
As regras estão em `nota-diaria.md`, `titulos.md`, `conceitos.md` e
`fotos.md`; isto aqui é só a demonstração delas.

## Como usar este arquivo

- **Regra ganha do exemplo.** Se algo aqui contradisser um `reference/*.md`,
  a regra vale e o exemplo está desatualizado — corrija o exemplo.
- **Nunca copie conteúdo daqui para uma nota real.** O assunto é Docker por
  acaso; se a sessão real também for de Docker, escreva do bruto do usuário,
  não daqui. O que se imita é a forma, nunca a matéria.
- Este arquivo **não** é uma nota do vault: mora em `.claude/`, que o
  Obsidian não indexa. Não o mova para `tech-study-diario/`, não o linke em
  nenhuma nota, e nunca o trate como sessão de estudo a editar. Os IDs abaixo
  são fictícios.
- Se o template `templates/template-tech-study.md` mudar, atualize este
  exemplo junto.

---

## Entrada: `nota bruta tech.md`

```markdown
# Nota bruta

## O que estou estudando
docker comandos, diferenca de imagem e container

## Conceito (ordem de importância)
- Docker / Linux

## Estudo
- docker pull baixa imagem do registry, se n falar a tag vem latest
- docker images lista as que ja tem aqui
- docker ps só mostra o q ta rodando, com -a aparece os parados tb
- tentei docker log deu erro q n existe o comando, é docker logs com s

acho q finalmente entendi a parada de imagem e container. a imagem é tipo a
receita, um negocio parado q nao executa nada, e o container é o prato feito
a partir dela. da mesma imagem eu posso fazer vários container ao mesmo tempo
e eles nao se misturam. isso explica pq deu erro qnd tentei exec num container
q tava parado — se ele ta parado nao tem processo nenhum rodando ali dentro,
entao nao tem onde encaixar o comando

![[Pasted image 20260724151203.png]]
salvar: erro do exec em container parado

- nao entendi bem o q acontece com os arquivos qnd o container para
- video do fireship
```

Repare em duas coisas. O bruto **não** tem pontuação, capitalização, ordem nem
separação por seção — isso é trabalho da skill. E ele **mistura formatos**:
tópicos soltos para os comandos, parágrafo corrido no meio para o raciocínio.
Isso é normal e não deve ser uniformizado.

## Saída: `tech-study-diario/Comandos Docker e diferença entre imagem e container.md`

Título proposto a partir do campo livre e confirmado com o usuário antes de
criar o arquivo (`titulos.md`).

```markdown
---
tipo: tech-study
data: 2026-07-24
tags:
  - tech-study
conceito: ["[[Docker]]", "[[Linux]]"]
id_obsidian: 20260724-151740
id_pai: 20260724-110454
---

# 📅 Comandos Docker e diferença entre imagem e container

## 📚 O que estudei hoje

%%--- INÍCIO AUTO-GERADO ---%%
- [[Docker]] — comandos básicos de imagem e container, e a distinção entre os dois.
- [[Linux]] — uso de shell interativo dentro de um container.
%%--- FIM AUTO-GERADO ---%%

## 📖 Conteúdo

%%--- INÍCIO AUTO-GERADO ---%%
Uma **imagem** é um snapshot imutável — a receita. Ela não executa nada por
conta própria. Um **container** é uma instância em execução criada a partir
dessa receita, e da mesma imagem podem sair vários containers simultâneos e
independentes entre si, sem que um veja o estado do outro.

Os comandos da sessão se dividem entre os que lidam com imagem e os que lidam
com container:

- `docker pull <imagem>[:tag]` — baixa a imagem do registry (Docker Hub por
  padrão) para o cache local. Sem tag explícita, assume `:latest`.
- `docker images` — lista as imagens já presentes na máquina.
- `docker ps` — lista os containers **em execução**; com `-a`, inclui também
  os parados e os que já saíram.
- `docker logs <container>` — mostra o stdout/stderr do container. O comando
  é no plural: `docker log` não existe.
- `docker exec -it <container> <shell>` — roda um comando novo dentro de um
  container **já em execução**; na prática, "entrar" no container para
  inspecionar. O `-i` mantém o stdin aberto e o `-t` aloca um
  pseudo-terminal: sem os dois não há shell utilizável.
%%--- FIM AUTO-GERADO ---%%

## 💡 Aprendizados / insights

%%--- INÍCIO AUTO-GERADO ---%%
Container parado não é um container "rodando de leve": não há processo nenhum
vivo dentro dele. Isso fechou duas coisas de uma vez — por que `exec` falha
ali (não existe processo ao qual anexar um comando novo) e por que a imagem
precisa ser algo separado do container, já que é ela quem guarda o estado
inicial quando não há nada em execução.
%%--- FIM AUTO-GERADO ---%%

## 🐞 Erros e como resolvi

%%--- INÍCIO AUTO-GERADO ---%%
- `docker log <container>` → o Docker não reconhece o comando → o subcomando
  é `docker logs`, no plural.
- `docker exec -it <id> bash` num container parado → erro do daemon dizendo
  que o container não está em execução → `exec` exige container up: rodar
  `docker start <id>` antes, ou criar um novo com `docker run`.

  ![erro do exec em container parado](fotos/foto-2026-07-24-15-12-03.png)
%%--- FIM AUTO-GERADO ---%%

## 🧠 Dúvidas / pontos a aprofundar

%%--- INÍCIO AUTO-GERADO ---%%
- [ ] O que acontece com os arquivos escritos dentro do container quando ele
      para? O que persiste e o que se perde (volumes vs. filesystem do
      container)?
%%--- FIM AUTO-GERADO ---%%

## 🔗 Recursos usados

%%--- INÍCIO AUTO-GERADO ---%%
- Vídeo do Fireship sobre Docker.
%%--- FIM AUTO-GERADO ---%%

## ❓ Autoteste

%%--- INÍCIO AUTO-GERADO ---%%
> [!question]- Qual a diferença entre imagem e container?
> A imagem é um snapshot imutável, a receita; o container é uma instância em
> execução criada a partir dela. Uma imagem serve de base para vários
> containers independentes.

> [!question]- Por que `docker exec` falha num container parado?
> Porque `exec` roda um comando novo dentro de um processo já em execução, e
> um container parado não tem processo vivo algum. É preciso `docker start`
> antes, ou criar outro container com `docker run`.

> [!question]- O que muda entre `docker ps` e `docker ps -a`?
> Sem `-a` só aparecem os containers em execução; com `-a` entram também os
> parados e os que já saíram.

> [!question]- Para que servem o `-i` e o `-t` em `docker exec -it`?
> `-i` mantém o stdin aberto e `-t` aloca um pseudo-terminal. Sem os dois não
> há shell interativo utilizável.
%%--- FIM AUTO-GERADO ---%%

## ✍️ Notas minhas

-
```

## O que este exemplo demonstra

- **📚 é escopo, 📖 é matéria.** O 📚 tem duas linhas e nenhum comando; toda a
  sintaxe está no 📖. Errado seria listar `docker pull, docker ps, exec` no 📚
  e deixar o 📖 vazio.
- **Prosa e lista convivendo.** O 📖 abre com um parágrafo (conceito, que pede
  encadeamento de ideias) e só então lista os comandos (itens enumeráveis, que
  pedem varredura visual). O 💡 é parágrafo puro. Transformar aquele parágrafo
  de abertura em três bullets — "imagem é imutável", "container é instância",
  "vários containers por imagem" — teria destruído exatamente o raciocínio que
  torna a distinção compreensível meses depois. Prosa não é enfeite aqui.
- **O registro do usuário foi respeitado.** No bruto, os comandos vieram em
  tópicos e o entendimento veio em parágrafo — e a nota manteve essa divisão.
  A skill reescreveu a linguagem, não a forma de pensar.
- **Nível do 📖.** `docker ps` não virou "lista containers" e pronto: virou o
  que faz, o que muda com a flag, e quando serve. É o nível mínimo aceitável.
- **💡 é insight, não definição.** "Docker facilita o desenvolvimento" seria
  resumo genérico e estaria errado ali. O que ficou é a conexão que o usuário
  fez na hora ("não há processo, logo `exec` não tem onde anexar") — algo que
  ele não sabia antes.
- **Seção opcional vazia desaparece.** O bruto não indicou nada concreto a
  fazer depois, então 🔁 "Próximos passos" **não existe** na nota — não ficou
  como título com bullet vazio.
- **Um trecho do bruto pode virar duas seções.** O parágrafo sobre imagem e
  container alimentou tanto a definição no 📖 quanto o insight no 💡, com
  redações diferentes; e o erro do `exec` alimentou 🐞 e virou pergunta no ❓.
  Isso é esperado — não é duplicação.
- **Foto.** A imagem do erro foi lida para escrever a mensagem em 🐞, foi
  renomeada para `fotos/`, e como o usuário escreveu `salvar:` embaixo dela,
  também entrou embedada logo abaixo do trecho que ela ilustra — com a legenda
  dele como alt.
- **🔗 sem exigência de precisão.** "Vídeo do Fireship" é suficiente: nada de
  pedir minutagem.
- **❓ sai só do 📖.** Nenhuma pergunta cobra volumes ou `docker compose` —
  assunto que a sessão não cobriu. E são perguntas de explicar, não de sim/não.
- **✍️ vazia**, sempre.
