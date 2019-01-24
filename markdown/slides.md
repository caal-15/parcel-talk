layout: true

---
class: middle, center, general
# Empaquetado para la web
## Una introducción usando Parcel y React
Una pequeña charla por [Carlos González](http://caal-15.github.io)

Síguela en [caal-15.github.io/parcel-talk](http://caal-15.github.io/parcel-talk)
.footnote[.alt-link[[Página Web de Parcel](https://parceljs.org/)]]

---
class: center, middle

# Conceptos Básicos

---
class: left, middle

# Empaquetado

.big[
  El _empaquetado_ o _bundling_ son una serie de procesos que pretenden preparar
  nuestro código _JavaScript_ que ha de correr en el navegador (__Client Side__)
  para un ambiente __productivo__.
]

---
class: left, middle

# Minificación

.big[
  La _Minificación_ de nuestro código es uno de los procesos más comunes, y
  consiste en reemplazar los __símbolos__ de nuestro código (nombres de
  funciones y variables), de manera que sean representados por pocos caracteres.

  Igualmente remueve espacios y saltos de línea innecesarios (este concepto
  se puede aplicar también a _CSS_ y _HTML_).
]

.footnote[.alt-link[[Parcel usa Terser para minificar tus archivos!](https://github.com/fabiosantoscode/terser)]]

---
class: left middle

# Ejemplo de Minificación

```javascript
function superFunction (anArg) {
  var toPrint = 'Will print: ' + anArg
  console.log(toPrint)
}

# Minificado:
function superFunction(n){var o="Will print: "+n;console.log(o)}
```

---
class: left middle

# Transpilación

.big[
  Usualmente por motivos de __compatibilidad__ debemos hacer uso de herramientas
  que traduzcan de los estándares mas nuevos de __ECMAScript__ (_ES7_, _ES6_) a
  los más  antiguos (_ES5_), este proceso se conoce como _transpilar_ nuestro
  código.
]

.footnote[.alt-link[[Una de las herramientas mas usadas es Babel](https://babeljs.io/)]]

---
class: left middle

# Ejemplo de Transpilación

```javascript
const superFunction = (anArg) => {
  const toPrint = 'Will print: ' + anArg
  console.log(toPrint)
}

# Transpilado:
function superFunction(anArg) {
  var toPrint = "Will print: " + anArg;
  console.log(toPrint);
};
```

---
class: left middle

# Versionado

.big[
  Para poder aplicar reglas de _caching_ y efectivamente actualizar nuestro
  código debemos __versionar__ nuestros assets, básicamente cambiando su nombre,
  usando un _hash_, o tal vez la fecha de generación.

  El _HTML_ y archivos que contengan referencias deben ser __actualizados__.
]

---
class: left middle

# Ejemplo de Versionado

.big[__Directorio:__]

```javascript
assets/
| javascript/
| | bundle20180809.js
```

.big[__HTML:__]

```html
...
<script src="/js/bundle20180809.js"></script>
...
```

---
class: left middle

# Partición de Código (Code Splitting)

.big[
  En ocasiones es necesario que nuestro __código__ no se cargue completamente,
  sino que se vayan cargando __paquetes__ del mismo a medida que sea
  _necesario_.

  Al proceso de crear los paquetes se le conoce como _Code Splitting_.
]

---
class: left, middle

# Procesos Sobre otros Assets

.big[
Algunos otros procesos sobre otros __Assets__ incluyen:

* _Transpilado_ de __CSS__ (SCSS, Stylus, etc.)
* _Prefijado_ de __CSS__ con prefijos de __propietario__.
* _Minificación_ de __CSS__ y __HTML__.
]

.footnote[.alt-link[[Parcel utiliza también PostCSS para gran cantidad de procesos](https://postcss.org/)]]
---
class: center, middle

# Parcel

---
class: left, middle

# Instalación

```bash
npm install parcel-bundler
# or
yarn add parcel-bundler
```

---
class: left, middle

# Procesos incluidos

.big[
* _Transpilación_ (__SCSS__ a CSS, __Babel__ para JavaScript).
* _Code Splitting_ (Nativo, Usando _dynamic imports_).
* _Autoprefixing_, otros procesos de CSS.
* _Minificación_ (HTML, CSS, JavaScript).
* _Versionado_ (CSS, JavaScript, Actualización automática de __Referencias__).
]

---
class: left, middle

# Cómo referenciar tus archivos
## Uso de Referencias relativas

.big[
Para hacer referencia a cualquier tipo de _asset_ desde uno de los archivos
que __parcel__ empaquetará solo debes usar _referencias relativas_:
]

```html
...
<script src='../src/index.js'></script>
...
```

---
class: left, middle

# Configuración

.big[
_Parcel_ pretende ser un __bundler__ completo para todo tipo de assets
(_JavaScript_, _CSS_, _HTML_), con la menor cantidad de configuración posible!,
puedes empezar __sin__ un archivo de configuración, al menos para proyectos
que no contienen _React_ :P.

A continuación cubriremos la configuración básica para los procesos de interés.
]

---
class: left, middle

# Transpilación: Babel

.big[
Para configurar Babel, lo hacemos simplemente utilizando _.babelrc_, no hay
necesidad de nada más!, una configuración tradicional podría ser:
]

```javascript
{
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
}
```

---
class: left, middle

# Code Splitting: Dynamic Imports

.big[
Como dijimos, _Parcel_ utiliza __Dynamic Imports__ para hacer
__code splitting__, y en _React_, puedes utilizar __Dynamic Imports__ con
componentes usando _lazy_.
]

```javascript
const OtherComponent = React.lazy(
  () => import('./OtherComponent')
)
const MyComponent = () => {
  return (
    <div>
      <OtherComponent />
    </div>
  )
}
```

---
class: left, middle

## Code Splitting Tip

.big[
Puedes mostrar un __placeholder__ mientras carga tu componente usando
_Suspense_!
]

```javascript
const OtherComponent = React.lazy(
  () => import('./OtherComponent')
)
const MyComponent = () => {
  return (
    <div>
      <Suspense
        fallback={<div>Loading...</div>}
      >
        <OtherComponent />
      </Suspense>
    </div>
  );
}
```

---
class: left, middle

# Servidor de desarrollo

.big[
Parcel incluye un _servidor de desarrollo_ con __hot reloading__,
para inicializarlo solo debes conocer __tu punto de inicio__, (usualmente un
archivo _HTML_):
]

```bash
parcel index.html
```

.big[
Si ya tienes un servidor, puedes usarlo solo para construir tus _assets_:
]

```bash
parcel watch index.html
```

---
class: left, middle

# Archivos productivos

.big[
Finalmente para obtener nuestros _assets_ procesados para __producción__:
]

```bash
parcel build index.html
```

---
class: left, middle

# Funcionalidad Avanzada

.big[
_Parcel_ También permite gran cantidad de __personalización__ a través de su
__API__, para necesidades más avanzadas, los invito a pegar un vistazo a la
.alt-link[[documentación](https://parceljs.org/api.html)]
]

---
class: center, middle

# Ahora a practicar!, Muchas Gracias por su Atención.

.footnote[_Me pueden invitar una cerveza despúes de la charla_]
