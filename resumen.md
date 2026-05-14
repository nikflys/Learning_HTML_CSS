# Conceptos clave para un proyecto web

Guía de referencia rápida. No reemplaza la práctica, pero ayuda a tener todo en un solo lugar.

---

## Índice

1. [Cómo funciona una página web](#1-cómo-funciona-una-página-web)
2. [HTML — Estructura](#2-html--estructura)
3. [CSS — Estilo](#3-css--estilo)
4. [JavaScript — Comportamiento](#4-javascript--comportamiento)
5. [Buenas prácticas generales](#5-buenas-prácticas-generales)
6. [SEO básico](#6-seo-básico)
7. [Accesibilidad web](#7-accesibilidad-web)

---

## 1. Cómo funciona una página web

Una página web tiene tres capas bien definidas:

| Capa | Tecnología | Para qué sirve |
|---|---|---|
| Estructura | HTML | Qué elementos hay y en qué orden |
| Presentación | CSS | Cómo se ven esos elementos |
| Comportamiento | JavaScript | Qué hacen cuando el usuario interactúa |

Cuando escribís una URL en el navegador, el navegador le pide el archivo al servidor, el servidor responde con el HTML, y el navegador lo lee de arriba a abajo y va construyendo la página. Si encuentra referencias a CSS o JS, los pide también.

---

## 2. HTML — Estructura

### Estructura mínima de un archivo HTML

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Título de la pestaña</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- Acá va el contenido visible -->
</body>
</html>
```

- `<!DOCTYPE html>` — le dice al navegador que es HTML5
- `<head>` — información sobre la página, no se muestra en pantalla
- `<body>` — todo lo que el usuario ve
- `lang="es"` — importante para lectores de pantalla y SEO
- `charset="UTF-8"` — permite tildes y caracteres especiales
- `viewport` — necesario para que la página se vea bien en celular

---

### Etiquetas más usadas

#### Texto
```html
<h1>Título principal</h1>   <!-- Solo uno por página, clave para SEO -->
<h2>Subtítulo</h2>          <!-- h1 a h6, de mayor a menor importancia -->
<p>Párrafo de texto.</p>
<span>Texto inline</span>   <!-- No genera salto de línea, útil para estilar parte de un texto -->
<strong>Negrita semántica</strong>
<em>Cursiva semántica</em>
```

#### Listas
```html
<ul>                         <!-- Unordered list: lista sin orden (bullets) -->
    <li>Elemento</li>
</ul>

<ol>                         <!-- Ordered list: lista numerada -->
    <li>Primer paso</li>
    <li>Segundo paso</li>
</ol>
```

#### Links e imágenes
```html
<!-- href puede ser una URL absoluta o una ruta relativa -->
<a href="pagina.html">Link interno</a>
<a href="https://google.com" target="_blank">Link externo</a>
<!-- target="_blank" abre en pestaña nueva -->

<!-- alt es obligatorio: describe la imagen para SEO y lectores de pantalla -->
<img src="imagen.png" alt="Descripción de la imagen" loading="lazy">
```

#### Contenedores
```html
<div>Bloque genérico</div>        <!-- Elemento de bloque, ocupa toda la línea -->
<span>Contenedor inline</span>    <!-- Elemento inline, no rompe la línea -->
```

---

### HTML Semántico

Usar las etiquetas correctas en lugar de `div` para todo. Mejora el SEO y la accesibilidad.

```html
<header>     <!-- Encabezado de la página o de una sección -->
    <nav>    <!-- Zona de navegación principal -->
        <ul>
            <li><a href="#">Inicio</a></li>
        </ul>
    </nav>
</header>

<main>                      <!-- Contenido principal, solo uno por página -->
    <section>               <!-- Sección temática del contenido -->
        <article>           <!-- Contenido independiente (un post, una noticia) -->
            <h2>Título</h2>
            <p>Contenido...</p>
        </article>
    </section>
</main>

<aside>                     <!-- Contenido secundario (sidebar, anuncios, info extra) -->
</aside>

<footer>                    <!-- Pie de página -->
    <p>Copyright 2025</p>
</footer>
```

---

### Formularios

```html
<form action="/enviar" method="POST">

    <!-- label + input: siempre juntos para accesibilidad -->
    <label>Nombre
        <input type="text" name="nombre" placeholder="Tu nombre" required>
    </label>

    <label>Email
        <input type="email" name="email" required>
    </label>

    <label>Contraseña
        <input type="password" name="pass" required>
    </label>

    <!-- select: dropdown con opciones fijas -->
    <select name="rol">
        <option value="user">Usuario</option>
        <option value="admin">Admin</option>
    </select>

    <!-- textarea: campo de texto multilínea -->
    <textarea name="mensaje" rows="5" placeholder="Tu mensaje..."></textarea>

    <!-- fieldset + legend: agrupa campos relacionados -->
    <fieldset>
        <legend>Preferencias</legend>
        <input type="checkbox" name="newsletter" id="nl">
        <label for="nl">Quiero recibir novedades</label>
    </fieldset>

    <input type="submit" value="Enviar">
</form>
```

**Atributos importantes de los inputs:**
- `name` — identifica el dato cuando se envía al servidor
- `required` — campo obligatorio
- `placeholder` — texto de ejemplo que desaparece al escribir
- `type` — define el tipo: text, email, password, number, checkbox, radio, file, date, color, submit

---

### Tablas

```html
<table>
    <thead>              <!-- Encabezado -->
        <tr>             <!-- tr = fila -->
            <th>Nombre</th>   <!-- th = celda de encabezado -->
            <th>Edad</th>
        </tr>
    </thead>
    <tbody>              <!-- Cuerpo de datos -->
        <tr>
            <td>Juan</td>     <!-- td = celda de dato -->
            <td>25</td>
        </tr>
    </tbody>
    <tfoot>              <!-- Pie de tabla (totales, resúmenes) -->
        <tr>
            <td colspan="2">Total: 1 persona</td>  <!-- colspan: ocupa N columnas -->
        </tr>
    </tfoot>
</table>
```

---

## 3. CSS — Estilo

### Cómo se vincula con HTML

```html
<!-- Externo (recomendado) -->
<link rel="stylesheet" href="styles.css">

<!-- Interno (en el head) -->
<style>
    p { color: red; }
</style>

<!-- Inline (evitar, mezcla estructura con estilo) -->
<p style="color: red;">Texto</p>
```

---

### Selectores

```css
/* Por elemento */
p { color: red; }

/* Por clase (puede repetirse) */
.mi-clase { font-size: 16px; }

/* Por id (único por página) */
#mi-id { background: blue; }

/* Selector combinado */
.card p { color: gray; }       /* p que está dentro de .card */
.card > p { color: gray; }     /* p hijo directo de .card */
.card + p { color: gray; }     /* p que está justo después de .card */

/* Pseudoclases */
a:hover { color: orange; }     /* cuando pasás el mouse */
input:focus { outline: none; } /* cuando el input está seleccionado */
li:first-child { ... }         /* primer elemento de una lista */
```

---

### El modelo de caja (Box Model)

Todo elemento en CSS es una caja con estas capas de adentro hacia afuera:

```
┌─────────────────────────────┐
│           margin            │  ← espacio externo (no tiene color)
│  ┌───────────────────────┐  │
│  │        border         │  │  ← borde del elemento
│  │  ┌─────────────────┐  │  │
│  │  │     padding     │  │  │  ← espacio interno (del borde al contenido)
│  │  │  ┌───────────┐  │  │  │
│  │  │  │ contenido │  │  │  │
│  │  │  └───────────┘  │  │  │
│  │  └─────────────────┘  │  │
│  └───────────────────────┘  │
└─────────────────────────────┘
```

```css
/* Por defecto (content-box): width y height solo miden el contenido.
   El padding y el border SE SUMAN al tamaño final. */
.caja { box-sizing: content-box; }

/* Recomendado (border-box): width y height incluyen padding y border.
   Lo que definís es el tamaño total de la caja, más intuitivo. */
.caja { box-sizing: border-box; }

/* Truco común: aplicarlo a todo */
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
```

---

### Colores

```css
/* Por nombre */
color: red;
color: coral;

/* RGB */
color: rgb(255, 100, 50);

/* RGBA (con transparencia, 0 = transparente, 1 = opaco) */
color: rgba(255, 100, 50, 0.5);

/* HEX */
color: #ff6432;   /* formato largo */
color: #f64;      /* formato corto (cuando cada par se repite) */

/* HEX con transparencia (últimos dos dígitos) */
background: #000000aa;  /* negro al ~67% de opacidad */
```

---

### Tipografía

```css
p {
    font-family: 'Roboto', sans-serif; /* siempre poner fuente de respaldo */
    font-size: 16px;
    font-weight: 400;      /* 100 muy fino → 900 muy grueso, 400 normal, 700 negrita */
    font-style: italic;
    line-height: 1.5;      /* interlineado, 1.5 es cómodo para leer */
    letter-spacing: 0.5px; /* espacio entre letras */
    text-align: left;      /* left | right | center | justify */
    text-transform: uppercase;   /* uppercase | lowercase | capitalize */
    text-decoration: underline;  /* underline | line-through | none */
}
```

**Fuentes externas:** se pueden usar de Google Fonts o cargar localmente con `@font-face`.

---

### Fondos

```css
div {
    background-color: #eee;

    background-image: url('imagen.jpg');
    background-size: cover;        /* cubre todo el contenedor, puede recortar */
    background-size: contain;      /* entra completa, puede dejar espacios */
    background-position: center;   /* top | bottom | left | right | center */
    background-repeat: no-repeat;  /* por defecto repite en mosaico */
    background-attachment: fixed;  /* la imagen queda fija al hacer scroll (parallax) */

    /* Degradé lineal */
    background: linear-gradient(to right, #ff0000, #0000ff);
    background: linear-gradient(45deg, red, blue, green);

    /* Degradé radial (circular) */
    background: radial-gradient(circle, #fff, #000);
}
```

---

### Bordes

```css
div {
    border: 2px solid black;          /* grosor | estilo | color */
    border-top: 1px dashed red;       /* solo un lado */
    border-radius: 8px;               /* esquinas redondeadas */
    border-radius: 50%;               /* círculo perfecto si width = height */
}
```

Estilos de borde: `solid`, `dashed`, `dotted`, `double`, `none`.

---

### Espaciado

```css
/* Shorthand de 4 valores: top right bottom left (sentido horario) */
margin: 10px 20px 10px 20px;

/* Shorthand de 2 valores: top/bottom  left/right */
margin: 10px 20px;

/* Un solo valor: los cuatro lados iguales */
margin: 10px;

/* margin: auto centra horizontalmente (el elemento necesita width definido) */
margin: auto;

/* Lo mismo aplica para padding */
padding: 10px 20px;
```

---

### Unidades de medida

| Unidad | Tipo | Descripción |
|---|---|---|
| `px` | Absoluta | Píxeles, tamaño fijo |
| `%` | Relativa | Porcentaje del elemento **padre** |
| `em` | Relativa | Relativo al `font-size` del **elemento actual** |
| `rem` | Relativa | Relativo al `font-size` del **elemento raíz** (`html`) |
| `vh` | Relativa | 1% del alto de la ventana |
| `vw` | Relativa | 1% del ancho de la ventana |

**Regla general:**
- Texto → `rem` o `em`
- Espaciados → `px` o `rem`
- Contenedores → `%`, `vw`, `vh`
- Imágenes con tamaño fijo → `px`

---

### Sombras

```css
/* box-shadow: sombra de la caja completa
   valores: offset-x  offset-y  blur  spread  color */
box-shadow: 0 4px 10px 0 rgba(0,0,0,0.3);
box-shadow: 0 0 20px #000a;    /* difusa y centrada */

/* text-shadow: sombra del texto
   valores: offset-x  offset-y  blur  color */
text-shadow: 2px 2px 4px rgba(0,0,0,0.5);

/* filter: drop-shadow sigue la forma del contenido, ideal para PNG con transparencia */
filter: drop-shadow(0 0 10px #000);
```

---

## 4. JavaScript — Comportamiento

> Esta sección está pendiente. JavaScript es la tercera capa del desarrollo web: permite que la página reaccione a acciones del usuario, modifique el HTML/CSS en tiempo real, haga pedidos a servidores, valide formularios, y mucho más.

Se agrega más adelante una vez que empiece ese tema.

---

## 5. Buenas prácticas generales

### HTML
- Un solo `<h1>` por página
- Siempre poner `alt` en las imágenes
- Usar etiquetas semánticas en lugar de `div` para todo
- Los `id` deben ser únicos, las `class` pueden repetirse
- Indentar correctamente para que sea legible

### CSS
- Evitar estilos inline en el HTML
- Usar `box-sizing: border-box` desde el principio
- Nombrar las clases según lo que representan, no según cómo se ven (`.boton-principal` en vez de `.boton-rojo`)
- Organizar el CSS de manera consistente (primero lo general, después lo específico)
- Evitar el uso excesivo de `!important`

### General
- Separar bien las tres capas: HTML solo estructura, CSS solo estilo
- Guardar los archivos en UTF-8
- Testear en distintos navegadores

---

## 6. SEO básico

SEO (Search Engine Optimization): conjunto de prácticas para que la página aparezca bien posicionada en buscadores.

```html
<head>
    <title>Título claro y descriptivo — Nombre del sitio</title>

    <!-- Descripción que aparece bajo el título en Google -->
    <meta name="description" content="Descripción breve de la página (máx 160 caracteres).">

    <!-- Palabras clave (ya no es tan relevante hoy en día, pero no hace daño) -->
    <meta name="keywords" content="palabra1, palabra2, palabra3">

    <!-- Cómo debe tratar el buscador la página -->
    <meta name="robots" content="index, follow">

    <!-- Open Graph: cómo se ve cuando alguien comparte el link en redes -->
    <meta property="og:title" content="Título de la página">
    <meta property="og:description" content="Descripción corta">
    <meta property="og:image" content="imagen-preview.jpg">

    <!-- Favicon: el ícono de la pestaña -->
    <link rel="icon" href="favicon.png" type="image/png">
</head>
```

**Factores de SEO que maneja el HTML:**
- Un buen `<title>` único por página
- Un solo `<h1>` descriptivo
- Uso de etiquetas semánticas
- Atributos `alt` en las imágenes
- Estructura lógica de encabezados (h1 → h2 → h3)
- Velocidad de carga (lazy loading de imágenes, etc.)

---

## 7. Accesibilidad web

El objetivo es que la página pueda usarse por personas con discapacidades visuales, motoras o cognitivas. Los lectores de pantalla (software que lee el HTML en voz alta) dependen de que el HTML esté bien escrito.

```html
<!-- lang en el html para que el lector sepa el idioma -->
<html lang="es">

<!-- alt en imágenes -->
<img src="logo.png" alt="Logo de la empresa">

<!-- label siempre asociado a su input -->
<label for="email">Email</label>
<input type="email" id="email" name="email">

<!-- role y aria-* para elementos interactivos personalizados
     (cuando usás un div o span para hacer algo que no es su función natural) -->
<div role="button" aria-pressed="false" tabindex="0">Aceptar</div>

<!-- tabindex="0" permite que el elemento reciba foco con Tab del teclado -->
```

**Regla simple:** si el HTML está bien escrito y es semántico, el 80% de la accesibilidad viene sola.
