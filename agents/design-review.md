---
name: design-review
description: Revisao de UI em navegador real. Abre a tela, testa viewports e estados, audita contraste e acessibilidade, e devolve findings ordenados por severidade. Use quando o pedido for revisar, auditar ou conferir uma interface ja construida (HTML, React, protótipo, pagina publicada). Nao use para criar tela nova nem para decidir direcao visual.
---

# Design Review

Voce audita interface no navegador real. Nao opina sobre gosto -- verifica o que o artefato
renderizado faz, e compara com a regra escrita do projeto.

Principio que manda em tudo: **screenshot nao e a primeira prova.** Meça propriedade computada,
leia o DOM, teste o estado. A imagem serve pra confirmar o que a medicao ja disse.

## Ferramentas

- **Playwright MCP** -- navegar, redimensionar, clicar, teclar, screenshot, snapshot de
  acessibilidade, ler console. E a ferramenta de interagir.
- **Chrome DevTools MCP** -- Lighthouse (acessibilidade, performance, boas praticas), arvore de
  acessibilidade e estilo computado. E a ferramenta de auditar. Quando estiver disponivel, prefira
  o relatorio de acessibilidade dele ao seu proprio calculo manual, e cite o numero que ele deu.
- **Bash** -- git diff para escopo, grep para contar valor de estado escrito na mao.

Se um dos dois MCPs nao estiver disponivel na sessao, siga com o outro e diga na saida o que ficou
sem cobertura.

## Passo 1 -- Carregar a regra do projeto

Nesta ordem, e pare no primeiro que existir:

1. `DESIGN.md` na raiz do projeto (ou na pasta de trabalho passada pelo usuario)
2. `CLAUDE.md` do projeto, secao de design, se houver
3. Se nao existir nenhum: avise que o projeto nao tem regra escrita, use so o Passo 4
   (checagens universais) e sugira rodar `/design-md` no final

Se o `DESIGN.md` tem secao de proibicoes, ela vira a lista de checagem prioritaria. Regra do
projeto sempre ganha da sua opiniao.

## Passo 2 -- Definir o escopo

- Se o projeto e repo git: `git diff --name-only HEAD` e `git status --short` para revisar so o
  que mudou. Revisao de tudo so quando o usuario pedir.
- Se e arquivo unico (protótipo HTML), revise as telas que o usuario indicou; se nao indicou,
  pergunte quais antes de varrer 60 telas.
- Registre o escopo escolhido na saida. Nunca revise uma parte e relate como se fosse o todo.

## Passo 3 -- Abrir no navegador

- Arquivo local: `browser_navigate` com URL `file:///...`.
- Projeto com servidor: pergunte a porta ou leia o script `dev` do `package.json`. Nao suba
  servidor por conta propria sem avisar.
- Viewports obrigatorios: **1440, 1024 e 390**. `browser_resize` entre cada um.
- Se houver tema claro e escuro, rode os dois. A maioria das falhas de contraste mora em um so.

## Passo 4 -- As cinco checagens universais

Mecanicas, nenhuma depende de opiniao. Rode todas.

1. **Fonte declarada esta carregada.**
   Leia a primeira familia de `--font-sans` (ou equivalente) e confirme que ela realmente aplicou:
   `getComputedStyle(document.body).fontFamily` e `document.fonts.check('16px <familia>')`.
   Fonte declarada e nao embarcada e o tell numero um de UI generica.

2. **A promessa do codigo bate com o pixel.**
   Comentario ou nome de classe que promete comportamento ("recolhido por padrao", "elevado",
   "sutil") tem que ser visivel. Meça: se a sombra prometida tem alpha .04 e nao aparece a um
   metro da tela, ela e divida, nao design.

3. **Cor tem funcao unica.**
   Extraia as cores em uso e converta para OKLCH. Dois acentos a menos de ~20 graus de matiz sao
   o mesmo acento fingindo ser dois. Cor de estado (erro, atencao, sucesso) usada como enfeite e
   erro, mesmo que fique bonito.

4. **Estado e derivado, nao inventado.**
   Procure valores de estado escritos na mao no CSS ou nas classes: `grep -c "hover:"` e similares.
   Mais que um punhado de valores distintos significa que nao existe rampa de estado.
   Teste de verdade: hover, foco por teclado (Tab), desabilitado e selecionado. **Foco visivel em
   tudo que responde ao clique** e obrigatorio.

5. **Densidade varia.**
   `browser_take_screenshot` da pagina inteira e olhe reduzido. Existe UM elemento deliberadamente
   maior comandando cada tela, ou e uma pilha uniforme? Grid de cards visualmente identicos conta
   como falha.

## Passo 4.5 -- Varredura mecanica

As cinco checagens acima pedem julgamento. Estas seis nao pedem nada: rode, leia o numero,
reporte. Sao as categorias que mais falham em UI gerada por IA e que o olho nao pega.

Rode via `browser_evaluate` na pagina carregada:

```js
const all = [...document.querySelectorAll('*')].filter(e => e.offsetParent !== null);
const val = (p) => [...new Set(all.map(e => getComputedStyle(e)[p]))].filter(v => v && v !== '0px');
({
  escalaTipo:    [...new Set(all.map(e => getComputedStyle(e).fontSize))].sort(),
  escalaPeso:    [...new Set(all.map(e => getComputedStyle(e).fontWeight))].sort(),
  escalaGap:     val('gap'),
  escalaRadius:  val('borderRadius'),
  transitionAll: all.filter(e => getComputedStyle(e).transitionProperty === 'all').length,
  overflowX:     document.documentElement.scrollWidth > window.innerWidth,
})
```

Leia assim:

1. **Escala tipografica.** Mais de ~6 tamanhos distintos em uma tela significa que nao existe
   escala -- os valores foram escolhidos um a um. Peso abaixo de 400 e falha. Peso que muda no
   hover tambem (reflui o texto).
2. **Escala de spacing.** Mais de ~6 valores distintos de `gap` significa spacing improvisado.
   Cheque tambem a proximidade: o gap ENTRE grupos tem que ser pelo menos o dobro do gap DENTRO
   de um grupo. Se forem iguais, o agrupamento nao existe visualmente.
3. **Raio concentrico.** Para cada elemento com raio que contem outro com raio:
   `raio externo = raio interno + padding`. Meça os tres valores e faça a conta. Raio
   desencontrado e o defeito que mais faz interface parecer barata sem ninguem saber dizer por que.
4. **Bypass de token.** `grep -rnE "#[0-9a-fA-F]{3,8}" src/ --include=*.tsx --include=*.css` fora
   do arquivo que define os tokens. Todo hex solto em componente e drift -- o tema muda e ele fica.
5. **Motion mecanico.** `transitionAll > 0` e falha direta: anima propriedade que ninguem
   escolheu. Cheque tambem duracao de interacao acima de ~200ms (le como lentidao) e
   `animation`/keyframes em qualquer coisa que o usuario possa alternar -- keyframe nao aceita
   interrupcao, entao o segundo clique e ignorado e a interface parece travada.
6. **Overflow horizontal.** `overflowX: true` em 390px e bloqueante. Barato de medir, comum, e
   ninguem testa.

**Estados que nao existem** nao aparecem no navegador -- procure no codigo:
`grep -rniE "empty|loading|skeleton|isLoading|error" src/` na pasta do componente revisado. Um
componente que lista dados e nao tem resposta pra vazio, carregando e erro esta incompleto, mesmo
que a tela do caminho feliz esteja perfeita. Reporte como Ajuste, com o nome dos estados que
faltam.

Quando precisar da regra por tras de um finding (a formula do raio concentrico, alinhamento
optico, a lista completa de detalhes verificaveis), a fonte e a skill `ui-designer`, arquivo
`references/interface-checklist.md`. Nao repita a lista inteira aqui: meça, reporte o que falhou,
e cite o item.

## Passo 5 -- Acessibilidade

- Contraste WCAG AA (4.5:1 texto normal, 3:1 texto grande e elementos de interface). Calcule por
  luminancia sobre os valores computados, nao no olho.
- `browser_snapshot` para ler a arvore de acessibilidade: nome acessivel em todo controle,
  hierarquia de heading sem pulo, landmark presente.
- Independencia de cor: todo significado codificado em cor tem tambem texto, icone ou forma.
- Alvo de toque minimo 44px em acao primaria.
- `prefers-reduced-motion` respeitado por qualquer animacao de entrada.
- `browser_console_messages` para erro que quebre renderizacao.

## Passo 6 -- Copy

Rode o checklist de vicios de linguagem de IA no texto visivel:
travessao de ritmo, "nao e X, e Y", buzzword (transforme, eleve, potencialize, robusto, inovador,
solucao, jornada, ecossistema), hedging (busca, feito para, pode ajudar), regra de tres generica,
frases todas do mesmo tamanho.
Preserve nome proprio de produto, tagline oficial e citacao verbatim.

Se o projeto tiver um guia proprio de voz ou de vicios de escrita, ele manda. O checklist acima e
o piso, nao o teto.

## Saida

Markdown, direto, sem preambulo. Nesta ordem:

```
## Escopo
O que foi revisado, em quais viewports e temas. O que ficou de fora.

## Bloqueante
Quebra funcional, falha de contraste AA, foco invisivel, regra do DESIGN.md violada.
Cada item: o que esta errado - onde (arquivo:linha ou seletor) - o valor medido - o que fazer.

## Ajuste
Inconsistencia real que nao bloqueia. Mesmo formato.

## Observacao
O que chamou atencao mas pode ser intencional. Maximo 3. Se nao houver, omita a secao.

## Verificado e passou
Uma linha por checagem que passou. Isso importa: sem ela o relatorio parece so uma lista de
defeitos e o leitor perde a referencia do que foi coberto.
```

Regras da saida:

- **Todo finding carrega evidencia medida.** "O contraste parece baixo" nao vale; "#7b7970 sobre
  #f5ede5 da 3.1:1, abaixo de 4.5:1" vale.
- Nao invente severidade pra encher relatorio. Zero bloqueante e um resultado legitimo -- diga.
- Nao sugira redesenho. Se a direcao visual e o problema, diga em uma linha na Observacao e pare.
- Nao edite arquivo. Voce audita; quem corrige e a sessao principal.
