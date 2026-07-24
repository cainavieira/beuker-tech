# Regras de match e criação de conceito

## Match por tema (não string exata)

Procure em `conceitos/*.md` um arquivo cujo título/tema corresponda ao
conceito listado no bruto — correspondência por tema, não string exata (ex.:
"Claude" no bruto pode casar com `conceitos/Claude Code.md` se for claramente
o mesmo assunto). Se houver mais de um candidato plausível, pare e pergunte
qual é, em vez de escolher sozinho.

## Conceito já existe

- Apenas linke: no corpo da nota tech-study (seção "O que estudei hoje") e no
  frontmatter `conceito:` (primeiro da lista do bruto = principal).
- **Nunca edite o arquivo do conceito.** As seções "O que é isso", "Por que
  estou estudando isso", "Recursos" e "Notas soltas / dúvidas" são
  processamento pessoal do usuário, escritas com as próprias palavras dele —
  a skill nunca escreve nelas.
- Não mexa em "Dias de estudo" — o backlink automático do Obsidian a partir da
  nota tech-study já resolve isso.

## Conceito não existe

- **Pergunte sempre antes de criar** — nunca decida sozinho. Ex.: "Não
  encontrei nota de conceito para X. Crio um esqueleto vazio agora (a partir
  de `Template conceito.md`), ou você cria depois?"
- Se o usuário confirmar a criação:
  - Gere o arquivo em `conceitos/<Nome>.md` a partir de
    `templates/Template conceito.md`.
  - Preencha `id_obsidian` no frontmatter, formato `YYYYMMDD-HHMMSS` (data e
    hora local de criação do arquivo, até o segundo — se colidir com um
    `id_obsidian` já existente, acrescente sufixo `-2`, `-3`...). Se esse
    conceito for o principal da sessão, esse mesmo valor é o que vai em
    `id_pai` na nota tech-study — ver `reference/nota-diaria.md`.
  - Deixe as seções de conteúdo (O que é isso, Por que estou estudando,
    Recursos, Notas soltas/dúvidas) **vazias** — nunca preencha a partir do
    bruto.
  - Pergunte a qual MOC Area (`moc areas/*.md`) o conceito pertence, para
    preencher o frontmatter `area:` do conceito e sugerir adicionar
    `[[Conceito]]` em "Conceitos ativos" do MOC area correspondente. Nunca
    decida a área sozinho, e nunca mexa em "Conceitos dominados / revisão" —
    é julgamento de maturidade do usuário.
  - Se não existir nenhum MOC area que sirva, pergunte se cria uma nova (a
    partir de `templates/Template moc area.md`) ou deixa sem área por
    enquanto.

## Múltiplos conceitos

- A ordem de escrita no bruto é a prioridade — o primeiro item é o conceito
  principal e vai no frontmatter `conceito:` da nota tech-study; os demais
  entram como links adicionais em "O que estudei hoje".
- Cada conceito (principal ou não) passa pela mesma checagem de
  match/criação acima, individualmente.
