# Auditoria de layout -- script read-only

Roda em um frame e devolve a arvore com as propriedades de layout mais os problemas encontrados.
E read-only: nao altera nada no arquivo, entao pode rodar a qualquer momento sem risco.

**Quando rodar**: depois de montar ou editar qualquer estrutura, ANTES de dizer que esta pronto.
E antes de comecar um conserto, pra saber o que exatamente esta quebrado em vez de chutar.

## Script

Trocar `ROOT_ID` pelo id do frame. Para auditar o que esta selecionado no Figma, usar a variante do fim.

```js
const ROOT_ID = "COLE_O_ID_AQUI";
const MAX_DEPTH = 6;
const MAX_ROWS = 200;

const root = await figma.getNodeByIdAsync(ROOT_ID);
if (!root) return { erro: "no nao encontrado: " + ROOT_ID };

const rows = [];
const flags = [];
const foraDaGrade = (v) => typeof v === "number" && v % 4 !== 0;

function read(n) {
  const o = { type: n.type };
  try { o.w = Math.round(n.width); o.h = Math.round(n.height); } catch (e) {}
  try { o.sz = n.layoutSizingHorizontal + " x " + n.layoutSizingVertical; } catch (e) {}
  if ("layoutMode" in n && n.layoutMode !== "NONE") {
    o.dir = n.layoutMode;
    o.pad = [n.paddingTop, n.paddingRight, n.paddingBottom, n.paddingLeft].join("/");
    o.gap = n.itemSpacing;
    o.align = n.primaryAxisAlignItems + " / " + n.counterAxisAlignItems;
  }
  if ("layoutPositioning" in n && n.layoutPositioning === "ABSOLUTE") o.abs = true;
  if (n.type === "TEXT") o.autoResize = n.textAutoResize;
  return o;
}

function walk(n, depth, path) {
  if (rows.length >= MAX_ROWS) return;
  const p = path ? path + " / " + n.name : n.name;
  const info = read(n);
  info.path = p;
  rows.push(info);

  const kids = "children" in n ? n.children : [];
  const isAL = "layoutMode" in n && n.layoutMode !== "NONE";
  const paiAL = n.parent && "layoutMode" in n.parent && n.parent.layoutMode !== "NONE";

  if (n.type === "GROUP")
    flags.push("GROUP -- trocar por frame auto layout: " + p);
  if (kids.length > 1 && "layoutMode" in n && !isAL && n.type !== "COMPONENT_SET")
    flags.push("frame com " + kids.length + " filhos e sem auto layout: " + p);
  if (info.abs && paiAL)
    flags.push("layoutPositioning = ABSOLUTE dentro de auto layout: " + p);
  if (info.w !== undefined && (info.w < 1 || info.h < 1))
    flags.push("dimensao colapsada (" + info.w + "x" + info.h + "): " + p);
  if (n.type === "TEXT" && n.textAutoResize === "WIDTH_AND_HEIGHT" && info.sz && info.sz.indexOf("FILL") === 0)
    flags.push("TEXT com FILL sem textAutoResize = HEIGHT -- vai colapsar: " + p);
  if (isAL && [n.paddingTop, n.paddingRight, n.paddingBottom, n.paddingLeft].some(foraDaGrade))
    flags.push("padding fora da grade de 4 (" + info.pad + "): " + p);
  if (isAL && kids.length > 1 && n.primaryAxisAlignItems !== "SPACE_BETWEEN" && foraDaGrade(n.itemSpacing))
    flags.push("gap fora da grade de 4 (" + n.itemSpacing + "): " + p);
  if (paiAL && !isAL && n.type !== "TEXT" && info.sz && info.sz.indexOf("HUG") === 0)
    flags.push("HUG em no que nao e auto layout nem texto -- checar: " + p);

  if (depth < MAX_DEPTH) for (const c of kids) walk(c, depth + 1, p);
}

walk(root, 0, "");
return { flags: flags, nos: rows.length, truncado: rows.length >= MAX_ROWS, arvore: rows };
```

Variante para auditar a selecao atual (sem precisar do id):

```js
const sel = figma.currentPage.selection;
if (!sel.length) return { erro: "nada selecionado no Figma" };
const ROOT_ID = sel[0].id;
// ... resto identico
```

## Como ler a saida

`flags` vazio e o criterio de pronto. Cada flag tem um conserto direto:

| Flag | Conserto |
|---|---|
| `GROUP` | Recriar como `figma.createAutoLayout()` e reanexar os filhos. Group nao tem sizing nem padding |
| `frame com N filhos e sem auto layout` | So aceitavel se for canvas de posicionamento livre (ilustracao, mapa). Caso contrario, converter |
| `layoutPositioning = ABSOLUTE dentro de auto layout` | Quase sempre resto de no movido entre containers. Setar `layoutPositioning = 'AUTO'` e redefinir o sizing. Manter apenas se for overlay proposital (badge, close) |
| `dimensao colapsada` | Sizing herdado errado. Ver o pai: se e auto layout, `FILL`; se nao, `resize()` explicito |
| `TEXT com FILL sem textAutoResize = HEIGHT` | `node.textAutoResize = 'HEIGHT'` antes de aplicar FILL. Sem isso o texto vira um fio de largura ~0 |
| `padding / gap fora da grade de 4` | Arredondar pra escala 4/8/12/16/24/32. Se foi decisao consciente (optical fix de 2px), dizer qual e por que |
| `HUG em no que nao e auto layout nem texto` | Sizing invalido que sobrou de outro contexto. Trocar por `FIXED` + `resize()` |

## Depois da auditoria

1. Consertar as flags em um `use_figma` por grupo de problema, nao tudo de uma vez.
2. Rodar a auditoria de novo -- conserto de sizing costuma revelar o proximo problema escondido.
3. So entao `get_screenshot` do frame pai (nao `node.screenshot()` do no isolado, que engana).
