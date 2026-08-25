# Comando: Design Review

Roda uma revisao de interface em navegador real e devolve findings com evidencia medida.

Argumento opcional: o alvo. Pode ser caminho de arquivo, URL, nome de tela ou nada.
Sem argumento, revise o que mudou (git diff) ou pergunte qual e o alvo.

## O que fazer

1. **Delegue ao subagente `design-review`.** Ele tem o metodo completo -- regra do projeto,
   viewports, as cinco checagens, acessibilidade e copy. Passe no prompt:
   - o alvo (arquivo, URL ou escopo do diff)
   - a pasta do projeto, pra ele achar o `DESIGN.md`
   - qualquer restricao dita nesta conversa

2. **Enquanto ele roda, nao adiante trabalho.** Nao abra o navegador em paralelo nem chute
   findings. Espere o retorno.

3. **Ao receber, apresente o relatorio inteiro** -- ele ja vem formatado. Nao resuma a ponto de
   perder a evidencia medida; o numero e o que torna o finding acionavel.

4. **Ofereca a correcao, nao aplique sozinho.** Liste o que da pra corrigir agora e pergunte o
   que atacar. Excecao: se o pedido foi `/design-review --fix`, corrija os bloqueantes na
   ordem, um commit logico por vez, e mostre o diff.

## Quando o projeto nao tem DESIGN.md

O subagente vai avisar. Nesse caso, no fim do relatorio, ofereca rodar `/design-md` -- sem regra
escrita a revisao fica so nas checagens universais, e metade do valor se perde.

## Quando nao usar

- Tela que ainda nao existe: e trabalho de criacao, use a skill `/ui-designer`.
- Duvida de direcao visual ou de fluxo: `/ui-designer` ou `/ux-designer`.
- Problema de dado, performance de backend ou build: nao e design review.
