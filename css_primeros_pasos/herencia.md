## Selectores y herencia

La palabra CSS viene de _Cascading StyleSheets_, esto quiere decir: Hojas de Estilo en Cascada. La palabra **cascada** hace referencia a una propiedad **muy importante** de las hojas de estilo, y es que los estilos aplicados a un elemento padre son heredados por su hijo.

Por ejemplo:

```html
<ul style="color: red">
    <li>Inicio</li>
    <li style="color: blue">Experiencia</li>
</ul>
```

En este caso el color de la fuente "Inicio" aparecerá en rojo y la de "Experiencia" en azul.

> **Nota**: te recuerdo que **no está recomendado** aplicar los estilos usando atributos. En este caso lo he hecho así porque creo que queda más clara la explicación.a

Del mismo modo y como ya adelantábamos al principio del capítulo, si un estilo se define dos veces, el último definido será el que prevalecerá, por ejemplo si en nuestro fichero escribimos:

```css
/* main.css */
p { 
    color: orange; 
    font-size: 24px; 
} 
p { 
    color: green; 
}
```

En este caso el color de todas las etiquetas **&lt;p&gt;** será verde. 

Ocurre lo mismo si la misma regla está definida en dos hojas CSS distintas que hayan sido cargadas usando la etiqueta **&lt;link&gt;**, en este caso prevalence el estilo definido en la última hoja cargada.

Si por error definiésemos la misma propiedad dos veces en un elemento también prevalecerá la segunda, por ejemplo:

```css
/* main.css */
strong {
    background: orange;
    background: yellow;
}
```

En este caso el fondo de la etiqueta prevalecerá en amarillo como se puede ver aquí: [http://libro.cursohtml5desdecero.com/css/?lesson=2&snippet=1](css/?lesson=2&snippet=1).

## Predominancia del estilo más específico

Ya hemos visto que podemos aplicar los estilos de tres formas, estas formas son de menos a más específicas:

* Por nombre de etiqueta
* Por clase \(**class**\)
* Por identificador \(**id**\)

Si asignamos estilos a un elemento de diferentes formas siempre predominará el más específico, esto quiere decir por ejemplo que si definimos lo siguiente:

```html
<head>
    <style>
        #food { 
            color: green; 
        } 
        p { 
            color: orange; 
        }
    </style>
</head>
<body>
    <p id="food">Mi fruta favorita es el mango.</p>
    <p>Mi cereal favorito es el trigo</p>
</body>
```

La frase "**Mi fruta favorita es el mango**" aparecerá en color verde, dado que un identificador es más específico que el nombre de la etiqueta. Sin embargo "**Mi cereal favorito es el trigo**" aparecerá en naranja, porque el estilo más específico para esa etiqueta es el de la etiqueta "**p**".

> **Nota**: la especificidad se calcula de una manera más compleja como se puede ver en [este tutorial](http://learn.shayhowe.com/html-css/getting-to-know-css/#specificity), pero para este curso he preferido simplificarlo un poco. Luego nos ayudaremos con DevTools para ayudar a experimentar y entender mejor cómo se aplican los niveles de especifidad.

## Combinar selectores

Hasta el momento hemos visto cómo utilizar un selector para especificar un elemento, pero podemos combinar **cualquiera** estos selectores siguiendo las siguientes reglas:

* Si escribimos los selectores separados por un espacio estamos haciendo referencia a las etiquetas anidadas dentro de otras.
* Si añadimos los selectores sin separar por un espacio estamos haciendo referencia a un mismo elemento de una manera más específica.
* Para entender cómo se aplican los selectores debes leerlos de derecha a izquierda
* El último selector antes del caracter "**{**" será al que se le aplique el estilo.

De este modo podemos seleccionar todos los elemento HTML que contienen una clase predefinida, etc. En este ejemplo vamos a ver cómo combinar nombres de etiquetas HTML con clases:

```html
<head>
    <style>
        h1 span{
            color: red;
        }
        p.big{
            font-size: 2rem;
        }
        p.big span{
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1>Mi <span>Curriculum Vitae</span></h1>
    <p class="big"><span>Nombre</span>: Raúl Jiménez Ortega</p>
    <p class="big"><span>Lugar de nacimiento</span>: Málaga</p>
    <p>Fecha de nacimiento: 11/03/1984</p>
</body>
```

Aquí estamos indicando:

* Que el color del texto de las etiquetas **span** que sean descendientes \(no necesariamente hijos directos\) de las etiquetas **h1** aparezcan en rojo.
* Que los párrafos con que contengan la clase "**big**" tengan un tamaño de fuente de "**2rem**".
* Que el ancho de la fuente de las etiquetas **span** que sean descendientes de las etiquetas **p** con la clase **big** sea negrita.

Esto al principio puede parecer un poco lioso, pero al final verás que aprenderás a usarlo por sentido común.

> **Notas**: 

> 1. Del mismo modo podríamos hacemos combinaciones usando identificadores, aunque dado que un identificador es único para un elemento y es el más específico no debería ser necesario usarlo nunca.

> 2. Al combinar los selectores la especifidad cambia como podemos leer en el tutorial antes mencionado.

### Múltiples clases

Es habitual utilizar varias clases en un mismo elemento<sup>1</sup>, por ejemplo:

```html
<a class="btn btn-primary">Entrar</a>
```
A este elemento se le aplicarán los estilos de la clase "**.btn**" y la clase "**.btn-primary**".

Si se diese caso de que ambas clases especifican una misma propiedad, por ejemplo **color** predominará la de la última indicada, en este caso la de la clase "**.btn-primary**".

### Otros selectores

Por último añadir que se puede aplicar el mismo estilo a varios selectores o conjunto de selectores separándolos por una coma, por ejemplo

```css
.bold,
strong,
p.title{
    font-weight: bold;
}
```
Esto significa que tanto a las etiquetas con la clase "**bold**" como las "**&lt;strong&gt;**" como las "**&lt;p&gt;**" que contengan la clase "**title**" se les aplicará el estilo "**font-weight: bold;**".

También se puede usar el caracter "**&gt;**" para especificar un hijo directo de un elemento, y otros [pseudo-elementos](https://developer.mozilla.org/en/docs/Web/CSS/Pseudo-elements), pero no entraremos en estos detalles en este curso.

---
**Aclaraciones**:

1. Esto lo veremos frecuentemente si usamos herramientas como "[Bootstrap](https://es.wikipedia.org/wiki/Twitter_Bootstrap)" u otros [frameworks CSS](https://es.wikipedia.org/wiki/Framework_de_CSS).
