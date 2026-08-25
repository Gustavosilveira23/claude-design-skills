# DESIGN.md -- <produto>

> Template. Substitua tudo entre `<>` e apague as linhas de instrucao em bloco de citacao.
>
> A regra que faz este arquivo funcionar: **escrever por restricao, nao por descricao.**
> Descricao o agente ignora; restricao ele obedece.
>
> Ruim: `primary: #1B4DFF`
> Bom: `primary: #1B4DFF -- so CTA e estado ativo. Nunca background, nunca decorativo.
> Um por tela. Se voce quer dois, o layout esta errado.`
>
> Gere este arquivo com `/design-md`, nunca deixando a IA inferir os principios sozinha: ela
> produz tokens perfeitos e principios inventados, e o resultado parece certo demais pra
> levantar suspeita.

---

## 0. Fonte de verdade

> Primeiro de tudo, porque resolve a briga antes dela acontecer. Liste em ordem de precedencia.
> Em caso de divergencia vale o de cima, e o desvio deve ser avisado -- nunca silenciosamente
> "corrigido" para o lado errado.

1. `<arquivo executavel -- o codigo que roda>`
2. `<tokens extraidos dele>`
3. `<doc de principios>`
4. `<doc antigo ou board de design>` -- **referencia historica**, nao copiar valor

## 1. O produto em tres frases

> O que faz, quem usa, o que a interface precisa conseguir. Vem antes de qualquer cor.
> Se voce nao consegue escrever isto, o resto vai sair generico.

<tres frases>

## 2. Os principios que decidem

> No maximo sete. O criterio nao e "isto e bonito", e sim: **quando duas solucoes empatam,
> qual ganha?** Principio que nunca desempatou nada nao e principio, e decoracao.

1. **<nome curto>.** <a regra, em uma ou duas frases>
2. ...

## 3. Tokens -- valor e fronteira

> Para cada grupo: o valor **e o limite**. O limite e a parte que importa -- e o que impede o
> agente de usar a cor de erro como enfeite porque ficou bonito.
> Regra geral: nenhum valor cru onde existe token. Se falta um numero, o token esta faltando.

### <grupo: superficie / texto / estado / marca>

<valores>

- <o que este grupo **nao** pode fazer>
- <quantos por tela, se aplica>

## 4. Tipografia

> Nao so a escala: **quando cada nivel entra e o que ele nao e.**

- Escala: `<fechada, com os degraus>`
- <regra de uso por nivel>
- <o que nunca acontece: peso fora da lista, tamanho arbitrario, etc.>

## 5. Logica de componente

> A pergunta nao e qual componente e mais bonito. E qual decisao a pessoa vai tomar ali.

| Situacao | Usa | Nao usa |
|---|---|---|
| <quando a pessoa percorre e escolhe> | <listagem> | <tabela com header, grid de cards identicos> |
| <quando precisa de parecer e acao> | <card com destino> | <card decorativo> |
| <quando ha muita informacao verdadeira mas nem toda necessaria agora> | <accordion> | <tudo aberto> |

## 6. Copy

- Idioma, pessoa e voz: `<...>`
- Termos travados (nao traduzir, nao sinonimizar): `<...>`
- **Proibido em copy de usuario:** `<labels internos, nome de arquitetura, jargao>`
- <regra de numero: categoria vs porcentagem, fato vs adjetivo>

## 7. Acessibilidade

> Liste as regras que **este** produto quebra com mais facilidade, nao a WCAG inteira.

- Contraste minimo `<AA / AAA>`; ponto historico de quebra: `<onde>`
- Independencia de cor: todo significado em cor tem tambem texto, icone ou forma
- Alvo de toque minimo `<44px>` em acao primaria
- `prefers-reduced-motion` respeitado por qualquer animacao de entrada

## 8. Proibicoes

> A lista curta. Cada linha tem que ser um **teste objetivo** -- alguem olha a tela e responde
> sim ou nao, sem discutir gosto. "Manter a elegancia" nao e proibicao; "sem gradiente" e.

- <...>
- <...>

## 9. Quality gate

> O que rodar antes de mostrar qualquer tela. Cinco checagens mecanicas cobrem a maior parte
> do que faz UI gerada por agente parecer generica:

1. **Fonte declarada esta carregada?** A familia em `--font-sans` aplicou de fato?
2. **A promessa do codigo bate com o pixel?** O que o comentario promete e visivel?
3. **Cada cor tem funcao unica?** Dois acentos a menos de ~20 graus de matiz sao o mesmo acento.
4. **Estado e derivado, nao inventado?** Hover, foco, disabled saem dos tokens?
5. **Densidade varia?** Existe UM elemento comandando a tela, ou e pilha uniforme?

Depois: checklist de copy e contraste nos dois temas.

## 10. Divida conhecida

> O que esta errado hoje, com o valor medido. Existe para **nao virar precedente**: quem chegar
> depois ve que e divida, nao permissao. Corrigir ao tocar na area.

- <desvio> -- <valor medido> -- <o certo>

---

*Escrito em <data> a partir de: `<arquivos>`. Metodo: regra por restricao, nao por descricao.*
