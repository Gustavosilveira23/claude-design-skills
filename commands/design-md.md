# Comando: Design MD

Gera o `DESIGN.md` de um projeto -- o arquivo que diz como o produto se parece e **o que e
proibido**. Ele fica na pasta onde o trabalho acontece, nao no vault, porque quem precisa ler e
o agente que vai mexer na tela.

## A regra que faz o arquivo funcionar

**Escrever por restricao, nao por descricao.**

Ruim: `primary: #1B4DFF`
Bom: `primary: #1B4DFF -- so CTA e estado ativo. Nunca background, nunca decorativo. Um por tela.
Se voce quer dois, o layout esta errado.`

Descricao o agente ignora. Restricao ele obedece.

## A regra que evita o desastre

**Voce extrai valor. A pessoa escreve o porque.**

Deixar a IA inferir principio a partir do Figma ou do CSS produz tokens perfeitos e principios
inventados -- o arquivo fica plausivel e errado, e ninguem percebe porque parece certo. Entao:

- Voce le o codigo e traz o **que existe**: tokens, escalas, familias, valores fora de padrao.
- Voce **entrevista** quem conhece o produto pelo **porque**: o que aquela cor pode e nao pode fazer, quando
  usar card e quando usar lista, o que nunca entra neste produto.
- Uma pergunta por vez, com opcao concreta quando der. Nada de questionario de 12 itens.

## Passo 1 -- Levantar o que existe

Antes de perguntar qualquer coisa, leia:

- tokens: `globals.css`, `tokens.css`, `tokens.json`, `tailwind.config`, variaveis CSS no `<head>`
- layout raiz: fonte carregada, tema forcado, provider
- componentes: quais existem, quais se repetem
- `CLAUDE.md` e docs de design que o projeto ja tenha, no repo ou no vault

E rode as varreduras que revelam divergencia -- elas rendem as melhores perguntas:

- escala de tipografia em uso e **valores arbitrarios** (`text-[...]`, `font-size` cru)
- valores de espacamento fora da grade declarada
- token declarado e **nunca usado** (grep no `src/`)
- mais de uma fonte de verdade para o mesmo valor (Figma x CSS x doc)

Traga esses achados para a conversa como pergunta, nao como acusacao: "achei sete tamanhos
arbitrarios de tipografia. A escala esta errada ou eles sao excecao proposital?"

## Passo 2 -- Entrevistar

Cubra, nesta ordem. Pule o que o projeto ja responde sozinho.

1. **O produto em tres frases.** O que faz, quem usa, o que a interface precisa conseguir.
   Vem antes de qualquer cor.
2. **Os principios que decidem.** Quando duas solucoes empatam, o que ganha? Maximo sete.
3. **Fronteira de cada token.** Nao o valor -- o limite. Onde essa cor nao pode aparecer.
4. **Tipografia com uso.** Quando cada nivel entra, e o que ele nao e.
5. **Logica de componente.** Quando card, quando lista, quando accordion. Decisao, nao aparencia.
6. **Copy.** Voz, pessoa, termos travados, palavras proibidas.
7. **Proibicoes.** A pergunta mais produtiva: *"o que voce ja teve que desfazer mais de uma vez
   neste projeto?"* -- e dali que sai a melhor lista.

## Passo 3 -- Escrever

Estrutura do arquivo, nesta ordem:

```
0. Fonte de verdade   ordem de precedencia; o que fazer quando divergem
1. O produto          tres frases
2. Principios         no maximo sete, o de cima ganha
3. Tokens             valor + fronteira, agrupados por intencao
4. Componente         quando usar o que, em tabela
5. Copy               voz e proibicoes
6. Acessibilidade     as regras que este produto quebra com mais facilidade
7. Proibicoes         lista curta, cada linha um teste objetivo
8. Quality gate       o que rodar antes de mostrar tela
9. Divida conhecida   o que esta errado hoje, pra nao virar precedente
```

Rodape com data e a lista de arquivos de onde cada valor saiu.

## Passo 4 -- Fechar

- Grave em `DESIGN.md` na raiz da pasta de trabalho.
- Se o projeto nao tiver `CLAUDE.md` ali, ofereca criar um curto: estado atual, onde mora a
  verdade, o que nao fazer. Curto de proposito -- os dois arquivos tem papeis diferentes e nao
  se repetem.
- Diga o que **voce nao soube responder** e ficou como pendencia no arquivo. Lacuna
  marcada vale mais que lacuna preenchida por chute.

## Regras

- Nenhum valor inventado. Todo numero rastreavel a um arquivo.
- Divergencia entre documento conceitual e arquivo executavel: vale o **executavel**, e avisar.
- Achou algo errado durante a leitura? Vai para a secao 9 como divida, com o valor medido.
  Nunca vira permissao.
