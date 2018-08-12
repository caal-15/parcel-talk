layout: true

---
class: middle, center, general
# Empaquetado para la web
## Una introducción usando Parcel
Una pequeña charla por [Carlos González](http://caal-15.github.io)

Síguela en [caal-15.github.io/ci-talk](http://caal-15.github.io/image-stitching-talk)
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

.footnote[.alt-link[[Uno de las herramientas mas usadas es Babel](https://babeljs.io/)]]

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
  sino que se vayan cargande __paquetes__ del mismo a medida que sea
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

---
class: center, middle

# Ahora a practicar!, Muchas Gracias por su Atención.

.footnote[_Me pueden invitar una cerveza despúes de la charla_]
