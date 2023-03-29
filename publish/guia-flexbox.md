# Guía sobre Flexbox

## RESUMEN de Propiedades Flexbox

###  Contenedor Padre (flex container)
- display: flex

- flex-direction
	- `row`
	- `column`
	- `row-reverse`
	- `column-reverse`

- flex-wrap
	- `wrap`
	- `no-wrap`
	- `wrap-reverse`

- flex-flow (flex-direction flex-wrap)


- justify-content
	- `normal`
	- `stretch`
	- `center`
	- `start` (según `writing-mode` o  `direction` del documento)
	- `end` (según `writing-mode` o `direction` del documento)
	- `flex-start` (según `flex-direction`)
	- `flex-end` (según `flex-direction`)
	- `space-between`
	- `space-around`
	- `space-evenly`
	- `left` (SIEMPRE lado izquierdo)
	- `right` (SIEMPRE lado derecho)
	- `safe` (items dentro de scroll)
	- `unsafe` (items fuera de scroll)

- align-items
	- `normal`
	- `stretch`
	- `center`
	- `start` (según `writing-mode` o  `direction` del documento)
	- `end` (según `writing-mode` o `direction` del documento)
	- `flex-start` (según `flex-direction`)
	- `flex-end` (según `flex-direction`)
	- `self-start` (según `writing-mode` o  `direction` del propio elemento padre)
	- `self-end` (según `writing-mode` o  `direction` del propio elemento padre)
	- `baseline`
	- `first baseline`
	- `last baseline`
	- `safe` (items dentro de scroll)
	- `unsafe` (items fuera de scroll)

- align-content (solo si `flex-wrap: wrap`)
	- `normal`
	- `stretch`
	- `center`
	- `start` (según `writing-mode` o  `direction` del documento)
	- `end` (según `writing-mode` o `direction` del documento)
	- `flex-start` (según `flex-direction`)
	- `flex-end` (según `flex-direction`)
	- `space-between`
	- `space-around`
	- `space-evenly`
	- `baseline`
	- `first baseline`
	- `last baseline`
	- `safe` (items dentro de scroll)
	- `unsafe` (items fuera de scroll)

- row-gap
	- `[0,∞]`, <length | percentage>

- column-gap
	- `[0,∞]`, <length | percentage>

- gap (row-gap column-gap)


### Contenedores Hijos (flex items)
- order
	- `[-∞,+∞]`

- flex-grow
	- `[0,∞]`

- flex-shrink
	- `[0,∞]`

- flex-basis
	- `0`
	- `auto`
	- `content`
	- `<length>`
	- `min-content`
	- `max-content`
	- `fit-content`

- flex (flex-grow flex-shrink flex-basis)


- align-self
	- `auto`
	- `normal`
	- `stretch`
	- `center`
	- `start` (según `writing-mode` o  `direction` del documento)
	- `end` (según `writing-mode` o `direction` del documento)
	- `flex-start` (según `flex-direction`)
	- `flex-end` (según `flex-direction`)
	- `self-start` (según `writing-mode` o  `direction` del propio elemento padre)
	- `self-end` (según `writing-mode` o  `direction` del propio elemento padre)
	- `baseline`
	- `first baseline`
	- `last baseline`
	- `safe` (items dentro de scroll)
	- `unsafe` (items fuera de scroll)

<br>
<br>
<hr>
<br>

## Algunas propiedades flexbox en profundidad

## __`flex-basis`__

Valores posibles para `flex-basis`:
- `0`
- `auto`
- `content`
- `min-content`
- `max-content`
- `fit-content`
- `length`

<br>

### Si `flex-basis: auto` y __existe__ `width`

El valor de `flex-basis` será el que marque `width`.

```css
.childItem {
	flex: 0 0 auto;
	width: 200px;
}
```

<br>

### Si `flex-basis: <auto | content>` y __NO__ existe `width`

El valor de `flex-basis` será `max-content` (el ancho del contenido).

```css
.childItem {
	flex: 0 0 auto;
}
```

<br>

### Si `flex-basis: <length>`

El ancho de la caja será el indicado por `<length>`

```css
.childItem {
	flex: 0 0 100px;
	width: 200px;
}

/* El ancho de .childItem sera 100px */
```

<br>

### Si `flex-basis: 0`

No se tendrá en cuenta el ancho del contenido en las cajas hijas como en `flex-basis: auto`. Dicho de otra forma, cogerá todo el ancho del contenedor padre para hacer el reparto.

- si `flex-grow: 0` el ancho de la caja hija será `min-content` __como máximo__ en las cajas que tengan estas propiedades.

- Si `flex-grow: (0 < x < 1)` la caja hija tendrá la parte proporcional del ancho total del contenedor padre. Si `flex-grow: 0.2` será la quinta parte del total como máximo, si `flex-grow: 0.33` la tercera parte como máximo, si `flex-grow: 0.5` la mitad del total como máximo, etc.

- Si `flex-grow: (>= 1)`
El ancho total del contenedor padre se repartirá entre las cajas hijas que tengan estas propiedades.


<br>
<br>

## __`flex-grow`__

Permite crecer a la caja hija hasta completar el ancho del contenedor padre. Si su valor es `0` la caja no crecerá.

Solo permite valores `<number>` positivos. Por defecto es `0`.

Mientras `flex-grow: 0`

- Si `flex-basis: 0` y __NO__ hay `width` su ancho será `min-content`.

- Si`flex-basis: auto` y hay `width` su ancho será el de `width`. Si no hay `width` será `max-content`.

- Si `flex-basis: <length>` su ancho será el indicado por `<length>`

Mienrtas `flex-grow: 0 < x < 1`

- La caja hija tendrá la parte proporcional __como máximo__ del ancho total del contenedor padre. Si `flex-grow: 0.2` será la quinta parte del total como máximo, si `flex-grow: 0.33` la tercera parte como máximo, si `flex-grow: 0.5` la mitad del total como máximo, etc.

Mientras `flex-grow: >= 1`

- Cualquier valor positivo por encima de `1` indicará el factor de crecimiento de la caja respecto del sus hermanos: `1` crecimiento normal, `2` crecimiento doble, etc.

- Si `flex-basis: 0` El ancho total del contenedor padre se repartirá entre las cajas hijas que tengan estas propiedades

- Si `flex-basis: auto` El espacio disponible en el contenedor padre se reparte entre las cajas hijas, sumándose al ancho del contenido de cada caja hija. 

- Si `flex-basis: <length>` Si la suma de todas las cajas hijas no superan el ancho total del contenedor padre, las cajas hijas crecerán.


<br>
<br>

## __`flex-shrink`__

Permite encojer las cajas hijas hasta el `min-content`. Si su valor es `0` la caja no crecerá.

Solo permite valores `<number>` positivos. Por defecto es `0`.

Mientras `flex-shrink: 0`

- Si `flex-basis: 0` su ancho será `min-content`.

- Si`flex-basis: auto` y hay `width` su ancho será el de `width`. Si no hay `width` será `max-content`.

- Si `flex-basis: <length>` su ancho será el indicado por `<length>`

Mienrtas `flex-shrink: 0 < x < 1`

- El espacio reducido irá en proporción a la ratio indicada. Así, si se indica que una caja tendrá un `flex-shrink: 1` y otra un `flex-shrink: .5` la última caja se reducirá la mitad que la primera.

Mientras `flex-shrink: >= 1`

- Cualquier valor positivo por encima de `1` indicará el factor de reducción de la caja respecto del sus hermanos: `1` reducción normal, `2` reducción doble, etc.

- Si `flex-basis: 0` Su ancho será `min-content`.

- Si `flex-basis: auto` Su ancho se reducirá en proporción al ratio indicado, siendo su límite `min-content`. 

- Si `flex-basis: <length>` Su ancho se reducirá en proporción al ratio indicado, siendo su límite `min-content`. 


<br>
<br>
<hr>

## Fuentes relacionadas
- [CSS-TRICKS A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [MDN Basic concepts of flexbox](https://developer.mozilla.org/es/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)
- [MDN Aligning items in a flex container](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Aligning_Items_in_a_Flex_Container)
- [MDN Controlling ratios of flex items along the main axis](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Controlling_Ratios_of_Flex_Items_Along_the_Main_Ax)
- [MDN Mastering wrapping of flex items](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Mastering_Wrapping_of_Flex_Items)
- [MDN Typical use cases of flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Typical_Use_Cases_of_Flexbox)
- [MDN Ordering flex items](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Ordering_Flex_Items)
- [MDN justify-content](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content)
- [MDN align-items](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items)
- [MDN align-content](https://developer.mozilla.org/en-US/docs/Web/CSS/align-content)
- [MDN align-self](https://developer.mozilla.org/en-US/docs/Web/CSS/align-self)
- [CSS LAYOUT NEWS Difference between start, flex-start, and self-start](https://csslayout.news/whats-the-difference-between-the-alignment-values-of-start-flex-start-and-self-start/)
- [W3C CSS Flexible Box Layout](https://www.w3.org/TR/css-flexbox-1/#box-model)
- [W3C CSS Box Alignment Module Level 3](https://www.w3.org/TR/css-align/#intro)
- [STACK OVERFLOW Flexbox: flex-start, self-start, and start; What's the difference?](https://stackoverflow.com/questions/50919447/flexbox-flex-start-self-start-and-start-whats-the-difference)
- [YT CSS WEEKLY In-Depth Guide to CSS Logical Properties](https://www.youtube.com/watch?v=cV9JhEV4Ll0)





[//]: # (FALTA INFO SOBRE:)
[//]: # (-----------------------)
[//]: # (- `baseline` )
[//]: # (- `first baseline`)
[//]: # (- `last baseline`)
