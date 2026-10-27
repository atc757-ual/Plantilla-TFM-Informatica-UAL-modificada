# Plantilla para el TFM para el Máster de Ingeniería Informática en la UAL

Versión revisada de la [plantilla original](https://github.com/savinspm/Plantilla-TFM-Informatica-UAL), con las correcciones y mejoras que surgieron al usarla para redactar un TFM completo. El contenido de ejemplo es el de la plantilla original, más un apartado nuevo sobre diagramas en TikZ.

## Compilar

```bash
latexmk -pdf main.tex
```

O el ciclo manual:

```bash
pdflatex main.tex && bibtex main && pdflatex main.tex && pdflatex main.tex
```

Requiere una distribución TeX Live o MiKTeX completa (usa, entre otros, `titlesec`, `pgfgantt`, `tikz` y `tabularx`). El resultado es `main.pdf`.

## Cambios respecto a la plantilla original

### Preámbulo (`main.tex`)

| Cambio | Por qué |
|---|---|
| `hyperref` se carga una sola vez y al final del preámbulo | Se cargaba dos veces y demasiado pronto: la segunda carga anulaba las opciones de la primera, y `hyperref` debe ir después de los paquetes cuyos comandos redefine (`titlesec`, `longtable`, `enumitem`, `footmisc`…). Enlaces activos en negro (para imprimir); para la versión digital basta cambiar `black` por `blue`. |
| `url` se carga por separado | `UAL.sty` usa `\UrlBreaks`, que antes llegaba a través de `hyperref`. |
| `graphicx` sin la opción `dvips` | No es compatible con `pdflatex`, que es como se compila la plantilla. |
| `emptypage` comentado | Solo tiene efecto con `twoside`; con `oneside` no hace nada. Se indica que se descomente junto con `twoside`. |
| Columnas elásticas `Y` y `Z` (`tabularx` + `array`) | Para que las tablas descriptivas ocupen el ancho del texto y hagan salto de línea en lugar de desbordarse o encogerse. |
| Estilos TikZ comunes (`\tikzset`) en el azul de la plantilla | Bloques, capas, flechas, secuencia, actividad, estados, entidad-relación, componentes, despliegue y clases UML con un mismo aspecto, listos para reutilizar. |
| Índices de figuras y tablas con el mismo formato que el índice general | Mismo interlineado y separación; las entradas no se descuadran. |
| Más ancho para el número de sección en el índice | A partir del capítulo 10, «10.1.» no cabía y el título quedaba pegado al número («10.1.Visión general»). |
| Sustitución de fuente declarada para negrita + versalita + cursiva | Los títulos con `\textit` dentro de `\scshape` generaban un aviso de fuente en cada uno; el resultado visual es el mismo y el registro queda limpio. |
| Bibliografía como capítulo del índice (`\cleardoublepage` + `\phantomsection`) | La entrada aparecía como sección del último capítulo y el enlace apuntaba a la página anterior. |

### Portada y contraportada

| Fichero | Cambio |
|---|---|
| `UAL.sty` | El título de la portada tiene más ancho y un tamaño menor (26 pt, negrita) para que los títulos largos quepan sin cortarse. |
| `contra.tex` | El resumen de la contraportada se ancla arriba a la izquierda del recuadro y con letra más pequeña, para que no se salga de él. |

### Índices y abreviaturas (`indicesyrefe.tex`)

- La tabla de abreviaturas usa `tabularx` a todo el ancho en lugar de `\resizebox`, que encogía la letra; los términos en inglés van en cursiva.
- Comentario junto a `\lstlistoflistings`: si la memoria no tiene bloques de código, genera una página vacía titulada «LISTADOS» y conviene comentarlo.

### Ejemplos (`contenido1.tex` y `diagramas/`)

- Nuevo apartado «Diagramas vectoriales con TikZ» con un ejemplo (`diagramas/ejemplo-capas.tex`) que usa los estilos comunes: un fichero por diagrama, incluido con `\input`.
- Cómo dar un título corto a los pies de figura largos (`\caption[corto]{largo}`), para que el índice de figuras no muestre párrafos enteros.

### Resultado

Con estos cambios la plantilla compila sin errores y con la mitad de cajas desbordadas que la original (las que quedan están en el texto de ejemplo de URLs largas).
