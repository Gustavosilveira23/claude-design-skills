# Comando: Estados

Pega UM componente e renderiza ele em todos os cenarios que a realidade consegue produzir, numa
pagina descartavel. A pagina e a entrega: a pessoa rola, ve os estados lado a lado, e o que
quebrou esta marcado ali.

Um componente construido contra um caminho feliz parece pronto ate o conteudo real chegar.

## O que este comando NAO e

- **Nao e `/design-review`.** Aquele julga uma tela construida contra a regra do projeto. Este
  provoca estados que ainda nao existem. Um audita, o outro estressa.
- **Nao e redesign.** Voce observa e reporta. Nao conserta sem pedido.
- **Nao e revisao de codigo.** Cenario previsto nao vale. So conta o que **renderizou e quebrou**
  na tela.

## Passo 1 -- Escopo: um componente

Um por rodada. "A tela de configuracoes" nao e componente; o campo de texto do formulario de
perfil e.

Se o pedido cobre varios, liste os candidatos e pergunte qual. Nao escolha pela pessoa.

Antes de construir, escreva em uma frase: o que o componente recebe, o que renderiza, e onde vai
viver.

## Passo 2 -- Escolher os eixos

Estresse so o que varia. Um eixo entra quando o componente aceita algo que pode ter aquela forma
em producao. **Leia o componente primeiro** -- props, slots, estados, os dados que renderiza.

| Eixo | Valores | Entra quando |
|---|---|---|
| **Quantidade** | zero, um, poucos, muitos, muitos + scroll | renderiza lista, tabela, grid ou colecao |
| **Carregamento** | carregando, carregado, erro, sem permissao | busca dado de fora |
| **Vazio** | vazio inicial, vazio depois de filtro, vazio depois do usuario limpar | tem estado de lista vazia |
| **Conteudo** | curto, longo realista, palavra sem quebra (URL/ID/email), caractere acentuado, numero grande com separador, data por extenso | recebe texto ou numero de fora |
| **Interacao** | padrao, hover, foco por teclado (Tab), pressionado, desabilitado, selecionado, invalido | responde a clique ou teclado |
| **Container** | estreito, natural, largo demais | a largura nao e fixa |
| **Ambiente** | tema claro, tema escuro, 390px, zoom 200% | o projeto tem tema ou e responsivo |

Dois cenarios que quase todo mundo esquece e que sao os que mais aparecem em uso real:

- **Vazio inicial e vazio depois de filtro sao telas diferentes.** "Nenhum projeto ainda -- criar
  o primeiro" nao serve pra "nenhum resultado pra 'xyz' -- limpar filtro". Se o componente
  responde a mesma coisa nos dois, e um achado.
- **Palavra sem quebra.** Um ID, uma URL ou um e-mail de 60 caracteres sem espaco. E o cenario
  que estoura layout com mais frequencia e o que menos aparece em dado de teste, porque dado de
  teste e sempre bem-comportado.

Escreva os cenarios escolhidos antes de construir, um por linha. Depois diga em uma linha quais
eixos voce descartou e por que -- assim uma inferencia errada custa barato.

## Passo 3 -- Montar a pagina

Uma pagina jogavel, com o componente **real importado do projeto**, renderizado uma vez por
cenario, em coluna unica, com um rotulo curto acima de cada instancia.

O componente vai **intocado, no ambiente real dele**:

- **Projeto React/Next:** uma rota de rascunho dentro do app (`app/lab/estados/page.tsx`). Ela
  herda layout, fontes e estilos globais de graca. Se o framework separa server de client, a
  pagina e client (`"use client"` no Next) -- prop de fixture some ao cruzar essa fronteira e
  todos os cenarios renderizam vazios.
- **Prototipo HTML puro:** um arquivo novo ao lado do original, com os **mesmos** `<link>` e
  `<style>` do prototipo, e o markup do componente copiado uma vez por cenario. Nao recrie o CSS,
  referencie o mesmo arquivo. Se o prototipo tem CSS embutido, copie o bloco inteiro sem editar.

A pagina so acrescenta rotulo, largura de container e dado de fixture. **Nao** acrescenta fonte,
estilo proprio, tema simulado ou troca de token -- componente observado sob qualquer uma dessas
coisas e outro componente.

Largura e cenario na pagina, nao redimensionamento: renderize as versoes estreita e larga dentro
de containers de largura fixa, ao lado da natural. Uma carga mostra todas.

Fixture nunca importa estado de producao, e producao nunca importa da pagina de teste.

## Passo 4 -- Olhar uma vez

Uma passada. Abra no navegador, role de cima a baixo, anote o que **visivelmente** quebrou.

"O texto passa da borda direita do card", nunca "o espacamento parece apertado". Julgamento de
gosto e trabalho do `/design-review` e da skill `ui-designer` -- aqui so entra o que a tela
mostrou.

Uma carga e o orcamento. Se nao houver navegador a mao, ou se ele exigir configuracao, **pule o
olhar**: entregue a URL e deixe quem pediu olhar. O olho de quem conhece o produto vale mais que
o seu aqui, e a pagina e dessa pessoa pra ler.

Depois marque cada quebra **na propria pagina**, uma linha embaixo do rotulo do cenario, numa
unica edicao. A pagina precisa se ler como relatorio sozinha.

## Passo 5 -- Reportar e parar

Tabela, cenarios quebrados primeiro:

```
| Cenario | O que aconteceu | Onde procurar a regra |
|---|---|---|
| Palavra de 60 caracteres sem espaco | Estoura o card, sem quebra e sem truncamento | interface-checklist, secao 2 |
| Zero itens | Regiao em branco, nenhuma mensagem | interface-checklist, secao 8 |
| Foco por teclado | Sem anel de foco visivel no botao secundario | interface-checklist, secao 7 |
```

A ultima coluna aponta onde mora a regra que diagnostica a quebra: a skill `ui-designer`,
arquivo `references/interface-checklist.md`. Este comando nao tem regra propria e nao da
veredito de gosto.

**"Tudo sobreviveu" e um relatorio completo e util.** Diga quais cenarios estao na pagina e onde
ela esta rodando, pra pessoa poder ver cada um. Termine ai, sem encher com preferencia.

Se pedirem pra consertar: siga a regra do `interface-checklist` (ou do `DESIGN.md` do
projeto, que ganha dela), conserte, e **re-renderize os cenarios que falharam** pra confirmar.

## Passo 6 -- Deixar a pagina de pe

A pagina e metade do relatorio, entao ela sobrevive a tabela. Deixe rodando. Apague ela e as
fixtures so quando disserem que terminaram.

## Erros que ja custaram retrabalho

| Erro | Correcao |
|---|---|
| Rodar todos os eixos em todo componente | So os eixos cujo gatilho bate; diga quais descartou |
| Reportar falha prevista como observada | Renderize, ou deixe de fora |
| Cenario renderiza vazio, sem o dado que recebeu | A pagina esta quebrada, nao o componente -- no Next, falta `"use client"` |
| Recriar um componente parecido na pagina de teste | Importe o real do projeto |
| A pagina re-estiliza ou re-tematiza o componente | Layout, fontes e tokens do app como estao; rotulo e largura e tudo que a pagina acrescenta |
| Redimensionar a janela cenario a cenario | Largura e container fixo na pagina; uma carga mostra todas |
| Achado escrito como gosto | Reporte o que apareceu na tela, ou nada |
| Quebra na tabela mas nao marcada na pagina | Anote embaixo do rotulo; a pagina se le sozinha |
| Apagar a pagina no mesmo turno do relatorio | A pagina e metade do relatorio; apague so quando pedirem |
| Tratar vazio inicial e vazio pos-filtro como um cenario so | Sao duas telas diferentes; teste as duas |
