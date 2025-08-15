# Guía paso a paso: construyamos la página hasta  🧑‍🏫

---

## 0) Preparación del proyecto

* Con el editor Visual Code Studio, Crea una carpeta: `sitioWeb/`
* Dentro, crea:

  * `index.html`
  * `assets/img/` (guarda aquí las imagenes necesarias para la construccion del sitio  )

> **Tip\:stas imagene**s se encuentran en la carpeta Recursos

---

## 1) Estructura HTML básica

**Objetivo:** partir de un documento HTML5 válido.

**Acción:** abre `index.html` y pega el esqueleto.

**Línea clave (parte del código a incluir):**

```html
<!doctype html><html lang="es"><head>...</head><body>...</body></html>
```

> Explicación: declaramos HTML5 (`<!doctype html>`), idioma en español (`lang="es"`), y abrimos `<head>` y `<body>`.

---

## 2) Metadatos mínimos y título

**Objetivo:** accesibilidad y correcto render en móviles.

**Línea clave:**

```html
<meta name="viewport" content="width=device-width, initial-scale=1"> <!-- responsive -->
```

> Explicación: asegura que el layout escale bien en pantallas pequeñas.

---

## 3) Incluir **Bootstrap 5** (CDN)

**Objetivo:** usar su sistema de grillas, utilidades y componentes.

**CSS (en ********************************************************************************************************************************************`<head>`********************************************************************************************************************************************):**

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"> <!-- Bootstrap CSS -->
```

**JS (antes de ********************************************************************************************************************************************`</body>`********************************************************************************************************************************************):**

```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script> <!-- Bootstrap JS -->
```

> Explicación: con el *bundle* ya tienes Popper y JS de componentes (como carrusel) sin instalar nada extra.

---

## 4) Barra superior (header simple con marca y menú)

**Objetivo:** reproducir el encabezado con la marca “Zay” y enlaces principales.

**Línea clave:**

```html
<nav class="navbar navbar-expand-lg bg-white border-bottom"><div class="container"><a class="navbar-brand fw-bold text-success" href="#">Zay</a> ... </div></nav>
```

> Explicación: `navbar-expand-lg` para menú colapsable en móviles, `text-success` aproxima el verde del logo.

**Código de ejemplo para el menú dentro del ********************************************************************************************`nav`********************************************************************************************:**

```html
<ul class="navbar-nav ms-auto">
  <li class="nav-item"><a class="nav-link" href="#">Home</a></li>
  <li class="nav-item"><a class="nav-link" href="#">About</a></li>
  <li class="nav-item"><a class="nav-link" href="#">Shop</a></li>
  <li class="nav-item"><a class="nav-link" href="#">Contact</a></li>
</ul>
```

### 4.1) Iconos en la barra y centrado del menú

**Objetivo:** agregar iconos (buscar, usuario, carrito) a la derecha de la barra y **centrar** las opciones del menú como en la imagen de referencia.

---

#### a) Incluir la librería de iconos

Usaremos **Bootstrap Icons** por simplicidad (CDN). Añádelo en el `<head>` **debajo del CSS de Bootstrap**:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css">
```

> Alternativa: Font Awesome. Pero con Bootstrap Icons tienes `bi bi-search`, `bi bi-person`, `bi bi-cart` sin instalar nada más.

---

#### b) Estructura de la barra con 3 zonas: marca / menú centrado / iconos

Reemplaza la estructura interna del `<nav>` por este patrón para alinear elementos:

```html
<nav class="navbar navbar-expand-lg bg-white border-bottom">
  <div class="container d-flex align-items-center">
    <!-- Marca a la izquierda -->
    <a class="navbar-brand fw-bold text-success me-3" href="#home">Zay</a>

    <!-- Botón hamburguesa -->
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#mainNavbar" aria-controls="mainNavbar" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <!-- Contenido colapsable ocupa todo el ancho -->
    <div class="collapse navbar-collapse" id="mainNavbar">
      <!-- MENÚ CENTRADO -->
      <ul class="navbar-nav mx-auto mb-2 mb-lg-0">
        <li class="nav-item"><a class="nav-link active" href="#home">Home</a></li>
        <li class="nav-item"><a class="nav-link" href="#about">About</a></li>
        <li class="nav-item"><a class="nav-link" href="#shop">Shop</a></li>
        <li class="nav-item"><a class="nav-link" href="#contact">Contact</a></li>
      </ul>

      <!-- ICONOS A LA DERECHA -->
      <div class="d-flex align-items-center gap-3">
        <a href="#search" class="text-dark"><i class="bi bi-search fs-5"></i></a>
        <a href="#account" class="text-dark"><i class="bi bi-person fs-5"></i></a>
        <a href="#cart" class="position-relative text-dark">
          <i class="bi bi-cart fs-5"></i>
          <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-success">3</span>
        </a>
      </div>
    </div>
  </div>
</nav>
```

* **`mx-auto`**\*\* en el \*\***`<ul>`** centra el menú.
* **`gap-3`** separa los iconos.
* **`badge`** crea el contador del carrito.

---

#### c) CSS opcional para apariencia (si lo quieres en tu propio archivo)

Crea `assets/style.css` y enlázalo en el `<head>`:

```html
<link rel="stylesheet" href="assets/style.css">
```

Contenido sugerido:

```css
/* Tamaño y color de los iconos */
.navbar .bi { vertical-align: middle; }
.navbar a.text-dark:hover { color: #198754; /* verde Bootstrap success */ }

/* Ajustes finos del badge del carrito */
.navbar .badge { font-size: .65rem; }

/* Centrado del menú en pantallas grandes (refuerzo) */
@media (min-width: 992px) {
  .navbar-nav { justify-content: center; }
}
```

> Nota: si no usas CSS externo, puedes mantenerlo con utilidades de Bootstrap (`mx-auto`, `gap-*`, `fs-*`, `text-*`, `position-*`).

---

#### d) Accesibilidad rápida

* Agrega `aria-label` a los enlaces de iconos si no tienen texto visible:

```html
<a href="#search" class="text-dark" aria-label="Buscar"><i class="bi bi-search fs-5" aria-hidden="true"></i></a>
```

---

## 5) Banner (carrusel) con imagen y texto

**Objetivo:** crear el banner superior como un **carrusel** con texto a la izquierda y una imagen a la derecha, tal como en la referencia.

### 5.1) Preparación de imágenes

Coloca 2–3 imágenes en `assets/img/` (por ejemplo: banner\_img\_01.jpg, `banner_img_02.jpg`, banner\_img\_03.jpg).&#x20;

**Línea clave:**

```text
assets/img/banner_img_01.jpg, assets/img/banner_img_02.jpg, assets/img/banner_img_03.jpg
```

---

### 5.2) Contenedor del banner dentro de la página

El carrusel irá en la sección **home** y dentro de un **container** para mantener márgenes.

**Línea clave:**

```html
<section id="home" class="py-5"><div class="container"> ... </div></section>
```

---

### 5.3) Estructura base del carrusel

Usaremos el componente de Bootstrap.

**Línea clave:**

```html
<div id="heroCarousel" class="carousel slide" data-bs-ride="carousel" data-bs-interval="5000">...</div>
```

**Bloque ejemplo (colócalo dentro del ********************************************************************************************`div.container`******************************************************************************************** del paso 5.2):**

```html
<div id="heroCarousel" class="carousel slide" data-bs-ride="carousel" data-bs-interval="5000">
  <div class="carousel-inner">
    <!-- Las diapositivas irán aquí -->
  </div>
</div>
```

> `data-bs-interval="5000"` cambia el tiempo (ms) entre diapositivas. Quita `data-bs-ride` si no quieres auto-rotación.

---

### 5.4) Indicadores (OPCIONAL)

Opcionales, pero útiles para navegación.

**Línea clave:**

```html
<div class="carousel-indicators"> <button data-bs-target="#heroCarousel" data-bs-slide-to="0" class="active"></button> ... </div>
```

**Bloque ejemplo (poner antes de ********************************************************************************************`.carousel-inner`********************************************************************************************):**

```html
<div class="carousel-indicators">
  <button type="button" data-bs-target="#heroCarousel" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
  <button type="button" data-bs-target="#heroCarousel" data-bs-slide-to="1" aria-label="Slide 2"></button>
  <button type="button" data-bs-target="#heroCarousel" data-bs-slide-to="2" aria-label="Slide 3"></button>
</div>
```

---

### 5.5) Diapositiva 1: texto + imagen

Cada **slide** es un `.carousel-item`. Dentro usamos grilla Bootstrap para dos columnas.

**Línea clave:**

```html
<div class="carousel-item active"><div class="row align-items-center g-4"> ... </div></div>
```

**Bloque ejemplo:**

```html
<div class="carousel-item active">
  <div class="row align-items-center g-4">
    <div class="col-lg-6">
      <h1 class="display-5 fw-bold">Zay <span class="text-success">eCommerce</span></h1>
      <p class="text-muted">Tiny and Perfect eCommerce Template</p>
      <a href="#shop" class="btn btn-success btn-lg">Shop Now</a>
    </div>
    <div class="col-lg-6 text-center">
      <img src="assets/img/banner_img_01.jpg" class="img-fluid" alt="Banner 1">
    </div>
  </div>
</div>
```

> `align-items-center` centra verticalmente el contenido de la fila.

---

### 5.6) Diapositivas 2 y 3 (repite el patrón)

Copia la estructura de la diapositiva 1, quita la clase `active` y cambia imagen/texto.

**Línea clave:**

```html
<div class="carousel-item"><img src="assets/img/banner-2.jpg" class="img-fluid" alt="Banner 2"></div>
```

**Bloque ejemplo:**

```html
<div class="carousel-item">
  <div class="row align-items-center g-4">
    <div class="col-lg-6">
      <h2 class="h1">Materiales modernos</h2>
      <p class="text-muted">Comodidad y estilo para todos los días.</p>
      <a href="#shop" class="btn btn-outline-success">Ver catálogo</a>
    </div>
    <div class="col-lg-6 text-center">
      <img src="assets/img/banner_img_02.jpg" class="img-fluid" alt="Banner 2">
    </div>
  </div>
</div>
<div class="carousel-item">
  <div class="row align-items-center g-4">
    <div class="col-lg-6">
      <h2 class="h1">Novedades</h2>
      <p class="text-muted">Descubre lo último de la temporada.</p>
      <a href="#shop" class="btn btn-outline-success">Explorar</a>
    </div>
    <div class="col-lg-6 text-center">
      <img src="assets/img/banner_img_03.jpg" class="img-fluid" alt="Banner 3">
    </div>
  </div>
</div>
```

---

### 5.7) Controles anterior/siguiente

Permiten navegar manualmente entre slides.

**Línea clave:**

```html
<button class="carousel-control-prev" data-bs-target="#heroCarousel" data-bs-slide="prev">...</button>
```

**Bloque ejemplo (colocar dentro de ********************************************************************************************`#heroCarousel`********************************************************************************************, después de ********************************************************************************************`.carousel-inner`********************************************************************************************):**

```html
<button class="carousel-control-prev" type="button" data-bs-target="#heroCarousel" data-bs-slide="prev">
  <span class="carousel-control-prev-icon" aria-hidden="true"></span>
  <span class="visually-hidden">Previous</span>
</button>
<button class="carousel-control-next" type="button" data-bs-target="#heroCarousel" data-bs-slide="next">
  <span class="carousel-control-next-icon" aria-hidden="true"></span>
  <span class="visually-hidden">Next</span>
</button>
```

---

### 5.8) Ajustes opcionales de altura/espaciado

Si quieres una altura mínima para el banner:

**Línea clave:**

```html
<section id="home" class="py-5" style="min-height: 420px;"> ... </section>
```

> También puedes controlar tamaños de texto con utilidades (`display-5`, `h1`, `h2`) y espaciados (`py-5`, `g-4`).

---

### 5.9) Accesibilidad y buenas prácticas

* Usa `alt` descriptivo en las imágenes.
* Mantén el texto clave fuera de la imagen para mejor legibilidad.
* Revisa contraste de colores (texto vs fondo).

> Con esto, el **banner-carrusel** queda listo con 2–3 diapositivas, cada una con **texto + imagen**.

---

## 6) Categories of The Month

**Objetivo:** construir la sección con **tres categorías** (imagen circular, título y botón “Go Shop”), centrada y responsiva.

### 6.1) Contenedor y encabezados

Coloca esta sección **después** del banner (carrusel).

**Línea clave:**

```html
<section id="categories" class="py-5 bg-light"><div class="container text-center"> ... </div></section>
```

**Encabezados dentro del contenedor:**

```html
<h3 class="fw-semibold">Categories of The Month</h3>
<p class="text-muted small mb-4">Excepteur sint occaecat cupidatat non proident...</p>
```

---

### 6.2) Fila responsiva

Creamos una fila con separación y centrado horizontal.

**Línea clave:**

```html
<div class="row g-4 justify-content-center"> ... </div>
```

---

### 6.3) Columna base (card transparente)

Cada categoría irá en su propia columna.

**Línea clave:**

```html
<div class="col-10 col-sm-6 col-lg-4"><div class="card border-0 bg-transparent text-center p-3"> ... </div></div>
```

> `col-10` centra en móvil, `col-sm-6` muestra 2 por fila en pantallas pequeñas, `col-lg-4` muestra 3 en escritorio.

---

### 6.4) Imagen circular (método rápido con estilos inline)

Usamos `rounded-circle` y forzamos tamaño cuadrado para mantener el círculo.

**Línea clave:**

```html
<img src="assets/img/category_img_01.jpg" class="rounded-circle img-fluid border" style="width:220px;height:220px;object-fit:cover;margin:auto;" alt="Watches">
```

**Alternativa con CSS (recomendado)**
Crea `assets/style.css`, enlázalo en el `<head>` y define una clase:

```html
<link rel="stylesheet" href="assets/style.css">
```

```css
/* assets/style.css */
.category-img { width: 220px; height: 220px; object-fit: cover; }
```

Ahora la imagen queda así:

```html
<img src="assets/img/watch.jpg" class="rounded-circle img-fluid border category-img" alt="Watches">
```

---

### 6.5) Título y botón por categoría

Añade el nombre y el botón “Go Shop”.

**Líneas clave:**

```html
<h6 class="mt-3 mb-2">Watches</h6>
<a href="#shop" class="btn btn-sm btn-success">Go Shop</a>
```

---

### 6.6) Repite para las otras categorías

Copia la **columna base** y cambia imagen/título:

**Shoes:**

```html
<img src="assets/img/category_img_02.jpg" class="rounded-circle img-fluid border category-img" alt="Shoes">
<h6 class="mt-3 mb-2">Shoes</h6>
```

**Accessories:**

```html
<img src="assets/img/category_img_03.jpg" class="rounded-circle img-fluid border category-img" alt="Accessories">
<h6 class="mt-3 mb-2">Accessories</h6>
```

> Consejo: verifica que las imágenes sean **cuadradas** para un círculo perfecto.

---

### 6.7) Codigo completo de la sección

Este bloque arma la sección completa con **tres columnas**.

```html
<section id="categories" class="py-5 bg-light">
  <div class="container text-center">
    <h3 class="fw-semibold">Categories of The Month</h3>
    <p class="text-muted small mb-4">Excepteur sint occaecat cupidatat non proident...</p>

    <div class="row g-4 justify-content-center">
      <!-- Category 1 -->
      <div class="col-10 col-sm-6 col-lg-4">
        <div class="card border-0 bg-transparent text-center p-3">
          <img src="assets/img/category_img_01.jpg" class="rounded-circle img-fluid border category-img" alt="Watches">
          <h6 class="mt-3 mb-2">Watches</h6>
          <a href="#shop" class="btn btn-sm btn-success">Go Shop</a>
        </div>
      </div>
      <!-- Category 2 -->
      <div class="col-10 col-sm-6 col-lg-4">
        <div class="card border-0 bg-transparent text-center p-3">
          <img src="assets/img/category_img_02.jpg" class="rounded-circle img-fluid border category-img" alt="Shoes">
          <h6 class="mt-3 mb-2">Shoes</h6>
          <a href="#shop" class="btn btn-sm btn-success">Go Shop</a>
        </div>
      </div>
      <!-- Category 3 -->
      <div class="col-10 col-sm-6 col-lg-4">
        <div class="card border-0 bg-transparent text-center p-3">
          <img src="assets/img/category_img_03.jpg" class="rounded-circle img-fluid border category-img" alt="Accessories">
          <h6 class="mt-3 mb-2">Accessories</h6>
          <a href="#shop" class="btn btn-sm btn-success">Go Shop</a>
        </div>
      </div>
    </div>
  </div>
</section>
```

---

### 6.8) Accesibilidad y pruebas rápidas

* Usa `alt` descriptivo en cada imagen.
* Revisa que en móvil se vean **1–2 columnas**, y en escritorio **3 columnas**.
* Verifica el contraste del botón y que el foco del teclado sea visible al tabular.

---

## Entrega y lineamientos finales

* El estudiante debe agregar el CSS que mejor considere para mejorar el aspecto de la página web, procurando que el resultado sea muy similar a la imagen propuesta.
* El estudiante debe completar las demás secciones del sitio siguiendo la estructura de los pasos anteriores y usando Bootstrap.
* Al finalizar, debe comprimir el proyecto (por ejemplo, la carpeta `sitioWeb/`) y subirlo al Aula Extendida.
