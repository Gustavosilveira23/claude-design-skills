# Comando: Variantes

Pega UM pedaco de UI e constroi tres versoes que discordam de proposito. Elas ficam atras de um
seletor **na pagina real**, e a pessoa alterna entre elas e escolhe.

Este comando nao julga. Ele produz candidatos e devolve a decisao. Quem julga tela construida e
o `/design-review`.

## Par com o `/estados`

| | Isola ou contextualiza? | Pergunta que responde |
|---|---|---|
| `/estados` | **isola** o componente | ele aguenta o conteudo real? |
| `/variantes` | **contextualiza** na pagina | qual direcao funciona aqui? |

Ordem natural: escolha a direcao com `/variantes`, promova a vencedora, depois estresse ela com
`/estados`. Variante que ganha no olho e quebra com texto longo nao ganhou nada.

## Respostas diferentes, nao tons diferentes

Tres variantes que mudam so a cor do acento nao ensinam nada. Voce alterna, nao ve escolha real,
e a rodada foi perdida.

Cada variante e uma **resposta diferente ao mesmo briefing**, num eixo:

| Eixo | O que varia | Skill que tem a regra |
|---|---|---|
| **Estrutura** | agrupamento, ordem, numero de colunas, o que colapsa | `ux-designer` |
| **Densidade** | escala de spacing, area de toque, quanto cabe | `ui-designer` |
| **Enfase** | onde vai cor preenchida, o que recua | `ui-designer` |
| **Tipografia** | degraus da escala, contraste de peso, medida | `ui-designer` |
| **Voz** | rotulos, tom, quanta copy | `ux-designer` |

**Escolha UM eixo primario** e de a cada variante uma posicao diferente nele. As decisoes
secundarias seguem dele, nao variam sozinhas -- uma variante densa pode pedir um degrau de tipo
menor, e isso e coerencia, nao um segundo eixo.

Variar tudo ao mesmo tempo produz tres resultados que nao se explicam. Quem pediu descobre de qual
gostou, nao o que fez funcionar, e a proxima tela comeca do zero de novo.

## O piso que toda variante tem que passar

Variante que ganha na aparencia e falha no basico nao e candidata, e bug com superficie bonita.

Antes de entrar no seletor, toda variante passa por:

- controle com nome acessivel
- teclado alcanca tudo que o ponteiro alcanca, e o foco e visivel
- nada corta em 390px
- nenhum significado carregado so por cor
- as proibicoes do `DESIGN.md` do projeto, se existir

O piso e **identico** nas tres. Nao e eixo e nunca troca contra um. Se uma direcao so funciona
quebrando o piso, diga isso e descarte a direcao.

A lista completa e verificavel esta na skill `ui-designer`, arquivo
`references/interface-checklist.md`.

## Passo 1 -- Escopo

Um pedaco por rodada. "O dashboard" nao e um pedaco; o card de metrica e.

Se o briefing cobre varios, aponte aquele de que os outros dependem, diga por que, e ofereca o
resto como rodadas futuras.

Reformule o briefing em uma frase: o que a coisa e, onde renderiza, o que precisa fazer.

## Passo 2 -- Ler o chao

Variante precisa parecer que pode subir amanha. Entao leia no que ela pisa:

- **`DESIGN.md` do projeto primeiro.** Ele diz o que e proibido, e proibicao limita quao longe a
  variante mais ousada pode ir. Sem ele, voce vai propor direcao que ja foi descartada.
- Sistema de estilo, biblioteca de componentes, biblioteca de motion.
- Tokens: cor, spacing, raio, escala de tipo, easing.
- Densidade e voz do produto. Uma ferramenta profissional densa limita a variante mais solta.
- Onde o pedaco renderiza: contra qual fundo, ao lado de quais vizinhos, em quais larguras.

Sem projeto pra ler: cinzas neutros, um acento, fonte de sistema -- e **diga que foi isso que
voce fez**.

## Passo 3 -- Nomear o eixo antes de escrever codigo

Tres variantes por padrao. Cinco so se pedirem ou se o espaco for genuinamente largo. Acima de
cinco ninguem compara, so rola a tela.

Escreva o conjunto antes: um nome e uma posicao no eixo para cada.

Nome diz qual e a **direcao**, nao a letra: `Silenciosa`, `Editorial`, `Densa` -- nunca
`Opcao A`.

Este passo termina quando duas variantes nao dividem a mesma posicao e voce consegue dizer o eixo
de cada uma em uma frase.

## Passo 4 -- Construir na pagina real

Variante fica boa isolada -- e por isso que isolado e o lugar errado de julgar. Hospede na pagina
que **vai conter** o pedaco, com o chrome real, os vizinhos reais e dado realista.

- **React/Next:** seletor por search param (`?variante=silenciosa`), assim cada variante e um link
  que da pra mandar pra alguem. Um controle flutuante troca.
- **Prototipo HTML:** o mesmo arquivo, com as variantes em blocos irmaos e um controle que
  alterna `hidden`. Mesmo CSS do prototipo, sem estilo novo.

O controle fica **visivelmente fora** do design system -- caixa fixa no canto, fundo solido,
fonte de sistema. Se ele parecer parte do produto, entra no julgamento.

Renderize **uma variante por vez, em tamanho real**. Miniatura distorce spacing e escala, e
spacing costuma ser exatamente a coisa que se esta escolhendo.

Conteudo real em todas: copy no formato do produto, nomes plausiveis, e a quantidade de itens que
a pagina vai carregar de verdade. Lorem ipsum e tres linhas fazem qualquer estrutura parecer boa.

## Passo 5 -- Apresentar o trade-off e parar

Passe por todas voce primeiro: cada uma renderiza, cada interacao responde, console limpo.

Depois entregue a decisao:

```
| Variante | Posicao no eixo | Boa quando | Custa |
|---|---|---|---|
| Silenciosa | menor peso visual | a tela e usada todo dia | menos memoravel |
| Editorial | tipo maior, mais respiro | o momento merece peso | come espaco vertical |
| Densa | mais itens por tela | comparar itens e a tarefa | cansa em sessao longa |
```

Diga onde o seletor esta rodando, como alterna, e **em qual largura voce julgou** -- a resposta
muda entre 390px e 1440px.

**Nao marque favorito na tabela.** A decisao de direcao e de quem conhece o produto e o cliente.
Se perguntarem direto qual voce escolheria, responda -- mas fundamente em frequencia de uso e
personalidade do produto, nunca em qual foi mais divertida de construir.

## Passo 6 -- Promover uma, apagar o resto

Escolhida a variante: construa ela direito onde ela mora, seguindo as convencoes do projeto,
apague as outras e apague o andaime.

Depois de promover, rode `/estados` nela. Foi escolhida no caminho feliz.

Se pedirem outra rodada: mantenha o andaime e repita o Passo 3, tomando posicoes novas em volta da
direcao que ficou mais forte.

Ate a promocao, o andaime nunca importa de producao e producao nunca importa do andaime.

## Erros que ja custaram retrabalho

| Erro | Correcao |
|---|---|
| Variantes diferem so no acento ou na copy | Mova uma pra outra posicao do eixo primario, ou corte |
| Todos os eixos variam de uma vez | Varie um; deixe o resto seguir dele |
| Julgado em rota em branco | Hospede na pagina que vai conter o pedaco |
| Lorem ipsum, tres linhas, "Fulano da Silva" | Copy real e a quantidade de itens que a pagina vai ter |
| A variante mais ousada pula teclado ou foco | Passe o piso ou descarte a direcao |
| Favorito marcado na tabela | Diga o custo de cada uma e deixe quem pediu escolher |
| Seletor estilizado com os tokens do projeto | Mantenha ele visivelmente fora do design system |
| Direcao proposta que o `DESIGN.md` ja proibe | Leia o `DESIGN.md` no Passo 2, antes de nomear os eixos |
| Andaime deixado pra tras depois de promover | Apague, a nao ser que peçam pra manter |
| Variante promovida sem passar pelo `/estados` | Ganhou no caminho feliz; estresse antes de considerar pronta |
