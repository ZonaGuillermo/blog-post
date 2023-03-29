# Tipo de Dato Numérico en CSS

Como en otros lenguajes de programación, CSS utiliza una serie de tipos de dato. Según sea el tipo de dato tendrémos una serie de valores y unidades que podrémos usar en las propiedades de CSS.

Existen los siguientes tipos de dato:
 - Textuales
 - Numéricos
 - Color
 - Imagen
 - Posicionamiento 2D

En este artículo nos centraremos en el tipo de dato Numérico.

<br>


## Tipos de dato _Numéricos_

Tenémos los siguientes:
 - `<integer>` - Usa valores enteros.
 - `<number>` - Usa valores reales.
 - `<percentage>` - Usa valores percentiles.
 - `<ratio>` - Define la proporción entre 2 valores sin unidad. Ej: 16/9
 - `<dimension>` - Su valor depende de la unidad asociada.

De todos estos cabe destacar `<dimension>` ya que para que los valores de este tipo de dato tengan sentido deben ir asociados a una unidad concreta. Estas unidades presentan en el siguiente apartado.

<br>


## Unidades de _Dimensión_

Las unidades de dimensión a su vez se agrupan en:

- Unidades de longitud `<length>`
- Unidades de Ángulo `<angle>` (`deg`, `rad`, `grad`, `turn`, `%`)
- Unidades de Tiempo `<time>` (`s`, `ms`, `%`)
- Unidades de Frequencia `<frequency>` (`Hz`, `kHz`, `%`)
- Unidades Flex `<flex>` (`fr`)
- Unidades de Resolución `<resolution>` (`dpi`, `dpcm`, `dppx` o `x`)

<br>


## Unidades de Longitud `<length>`

Este conjunto de unidades se dividen en unidades absolutas y unidades relativas.

Las __unidades absolutas__ se refieren a una longitud física, como centimetros (`cm`), puntos (`pt`) o pulgadas (`in`).

Mientras que las __unidades relativas__ expresan su valor en relación a otra cosa. Por ejemplo, `em` es relativa al tamaño de la fuente del elemento o `vh` relativa a la altura del viewport.

<br>

### Unidades Absolutas

CSS acepta las siguientes unidades absolutas indicadas abajo. Cabe destacar la siguiente equivalencia: __`1in = 96px = 72pt`__
 - Pixel: `px`
 - Pulgada: `in`
 - Centimetro: `cm`
 - Milimetro: `mm`
 - Cuarto de milimetro: `Q`
 - Pica: `pc`
 - Punto: `pt`

<br>

### Unidades Relativas a la fuente 

Encontramos la siguientes:
- `em`
- `rem`
- `ch`
- `ex`
- `cap` (experimental)
- `lh` (experimental)
- `rlh` (experimental)
- `ic` (experimental)


#### __`em`__
Su valor es relativo al tamaño de fuente del elemento. Si se usa en la propiedad `font-size` del propio elemento su valor dependerá del ancestro inmediatamente anterior que defina la propiedad `font-size`.

Hay que tener cuidado con esta unidad ya que su valor se puede ver afectado con otras declaraciones `em` situados en otros niveles anteriores de la jerarquía. Por ejemplo:

```html
<main>
	<article style="font-size: 30px;">
		<section style="font-size: 0.8em">
			<div>
				<h3 style="font-size: 32px">
					My title
				</h3>
				
				<p style="font-size: 0.5em;">
					Lorem, ipsum dolor sit amet consectetur adipisicing elit. Aperiam in, itaque iusto ad animi sequi.
				</p>
			</div>
		</section>
	</article>
</main>

<!-- 
	El elemento <p> tendrá un tamaño de fuente de 12px
	ya que 30px * 0.8em * 0.5em = 12px
-->
```

#### __`rem`__
Su valor es relativo al tamaño de fuente del elemento raíz ya sea `:root` o `<html>`. Si se usa en el `font-size`de la raíz establecerá el valor inicial para toda la web o app que por defecto es __16px__.


#### __`ch`__
Se refiere al __ancho del caracter '0'__ de la fuente usada en el elemento. Si no se pudiera determinar se considerará 0.5em de ancho por 1em de alto.


#### __`ex`__
Se refiere a la __altura del caracter 'x' minúsula__ (0.5em aprox.). Esta unidad rara vez se usa.


El resto de unidades, al ser experimentales aún, no se tratarán en este artículo.

<br>

### Unidades Relativas al viewport
 - v* (`vw`, `vh`, `vi`, `vb`, `vmin`, `vmax`)
 - sv* (`svw`, `svh`, `svi`, `svb`, `svmin`, `svmax`)
 - lv* (`lvw`, `lvh`, `lvi`, `lvb`, `lvmin`, `lvmax`)
 - dv* (`dvw`, `dvh`, `dvi`, `dvb`, `dvmin`, `dvmax`)

Estas medidas se refieren a las dimensiones del area de contenido de la ventana (viewport) en navegadores.

Las primeras en aparecer fueron las `v*`. `vw` se refiere al ancho de la ventana, mientras que `vh` se referirá al alto.

Con la llegada de las barras de navegación retráctiles en los navegadores de tablet y móviles (las que se esconden y vuelven a aparecer con el desplazamiento) surgió el problema de que en las aplicaciones o webs algunos elementos quedaban fuera de la vista en diseños a pantalla completa o solapados por la barra de navegación. Para solventar este problema surgieron nuevas unidades como las `sv*`, `lv*` y `dv*`.

Las `sv*` se refieren a las dimensiones de la ventana cuando la barra de navegación se __está mostrando.__

Las `lv*` se refieren a las dimensiones de la ventana cuando la barra de navegación está __oculta.__

Las `dv*` son unidades dinámicas. __Se ajustan automáticamente__ según la barra de navegación se esté mostrando o no.

Tras esta actualización, las unidades `v*` suelen coincidir con las `lv*` aunque depende de la implementación que haga cada navegador.

En cuanto a las unidades `*vi` y `*vb`, tienen en cuenta la dirección y sentido de la escritura. En una escritura de izquierda a derecha (__in-line axis__) y de arriba a abajo (__block axis__), `*vi` coincide con `*vw`, mientras que `*vb` coincidirá con `*vh`.

Sobre las `*vmin`y `*vmax`no hay diferencias de unas a otras según la [W3C](https://www.w3.org/TR/css-values-4/#viewport-relative-units). Las `*vmin` escogeran siempre el menor valor entre `*vw` y `*vh` y las `*vmax` el mayor valor.

<br>

### Unidades Relativas a las Container Querys
 - `cqw`
 - `cqh`
 - `cqb`
 - `cqi`
 - `cqmin` (cqb o cqi)
 - `cqmax` (cqb o cqi)

Especifican medidas relativas al __container query__. Un container query es un tipo de contenedor padre en donde sus contenedores hijos se dimensionan o se adaptan según las características del padre.

Un componente que usa este tipo de unidades puede trasladarse a otro contenedor padre, también de tipo container query, y adaptarse sin problemas.

Se evitan así problemas de mantenimiento y la necesidad de crear nuevas reglas específicas o incluso media queries para otro tipo de situaciones, como puede ser la vista para diferentes medios como desktop, tablets o móviles. Con una sola declaración lo abarcamos todo.

#### __`cqw`__ y __`cqh`__
Se refieren al % de ancho y alto respecto del contenedor padre (container query) respectivamente.

#### __`cqi`__ y __`cqb`__
Estas unidades se usan teniendo en cuenta la dirección y sentido de la escritura. En una escritura de izquierda a derecha y de arriba hacia abajo `cqi` se referirá al % de ancho (__in-line axis__) y `cqb` se referirá al % de alto (__block query__) siempre hablando respecto del contenedor padre (container query).

#### __`cqmin`__ y __`cqmax`__
`cqmin` se referirá siempre __al menor__ de los valores `cqi` o `cqb`. Mientras que `cqmax`se referirá __al mayor__ de los valores `cqi` o `cqb`.

<br>
<br>
<hr>

## Fuentes relacionadas
- [MDN CSS values and units](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Values_and_Units)
- [MDN \<length\> CSS Data Types](https://developer.mozilla.org/en-US/docs/Web/CSS/length#container_query_length_units)
- [MDN \<percentage\> CSS Data Types](https://developer.mozilla.org/en-US/docs/Web/CSS/percentage)
- [W3C The Various Viewport-relative Units](https://www.w3.org/TR/css-values-4/#viewport-relative-units)
- [CSS-TRICKS The trick to viewport units on mobile](https://css-tricks.com/the-trick-to-viewport-units-on-mobile/)
- [CYBMETA Como utilizar em y rem en CSS](https://cybmeta.com/em-y-rem)
- [MDN Learn CSS values and units: `em` & `rem` units](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units)
- [YT CSS Weekly: In-Depth Guide to CSS Logical Properties](https://www.youtube.com/watch?v=cV9JhEV4Ll0)