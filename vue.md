# ¿Qué es VUE.js?

Es un framework web progresivo que permite añadir reactividad a tus aplicaciones web. Ventajas de Vue.js:

* Accesible (si conoces HTML, CSS y JS es fácil de aprender)
* Versátil (posibilidad de usarlo como librería en una pequeña sección o construir una aplicación completa con su framework completo)
* Con alto rendimiento (20Kb de peso con un virtual dom optimizado)
* Mantenible

Comparativa con otros frameworks: https://es-vuejs.github.io/vuejs.org/v2/guide/comparison.html

# Estructura componente Vue

## Data binding

```{{ propiedad }}``` accederiamos desde el template a una propiedad del modelo.

$data: accedes a todo el modelo de datos del componente

## Eventos

Para linkar eventos a métodos del componente utilizaremos el atributo "v-on:<evento>".

También se puede definir con @:evento

Se pueden agregar diferentes comportamientos al evento:

* **Event modifiers**: posibilidad de definir diferentes comportamientos del evento como parar propagación, etc:

```html
<!-- the click event's propagation will be stopped -->
<a v-on:click.stop="doThis"></a>

<!-- the submit event will no longer reload the page -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- modifiers can be chained -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- just the modifier -->
<form v-on:submit.prevent></form>

<!-- use capture mode when adding the event listener -->
<!-- i.e. an event targeting an inner element is handled here before being handled by that element -->
<div v-on:click.capture="doThis">...</div>

<!-- only trigger handler if event.target is the element itself -->
<!-- i.e. not from a child element -->
<div v-on:click.self="doThat">...</div>
```

* **Key modifiers**: para eventos de teclado normalmente se necesita comprobar ciertas teclas. Vue permite indicar que tecla escucha ese evento:

```html
<input v-on:keyup.enter="submit">
<input v-on:keyup.page-down="onPageDown">
<input v-on:keyup.13="submit">
```

* **System modifiers keys**: para capturar combinaciones de eventos de raton y de teclado.

```html
<!-- Alt + C -->
<input @keyup.alt.67="clear">

<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
```

## Directivas

Atributos que proporcionan capacidades extras a elementos HTML

* v-model: binding de datos
* v-show: renderizado condicional sin eliminar el elemento del DOM
* v-if / v-else / v-else-if: renderizado condicional eliminando el elemento del DOM
* ```<template v-if="CONDICION">```: renderizado condicional para un bloque de template
* v-for: renderizado en bucle

```html
<li v-for="(tarea, index) in tareas">{{ index }} - {{ tarea.name }}</li>
```
&ensp;&ensp;&ensp;Se puede utilizar v-for para desestructurar un objeto

```html
<li v-for="(value, key, index) in object">{{ key }} : {{ value }}</li>
```

## Propiedades computadas

Cuando se realizan diferentes transformaciones o logica al momento de mostrar una propiedad, se debería crear una propiedad computada.

```javascript
computed: {
    mensajeAlReves() {
      return this.mensaje.split('').reverse().join('');
    }
  }
```
```html
<!-- Sin propiedad computada -->
<h3>{{ mensaje.split('').reverse().join('') }}</h3>
<!-- Con propiedad computada -->
<h3>{{ mensajeAlReves }}</h3>
```

## Filtros
A partir de la version 2.0 no existen los filtros nativos de Vue y deberás crearlos por ti mismo con **Vue.filter**

```javascript
Vue.filter('mensajeAlReves',(mensaje) => mensaje.split('').reverse().join(''))
```
```html
<!-- Sin filtro -->
<h3>{{ mensaje.split('').reverse().join('') }}</h3>
<!-- Con propiedad computada -->
<h3>{{ mensajeAlReves }}</h3>
<!-- Con filtro -->
<h3>{{ mensaje | mensajeAlReves }}</h3>
```


# Herramientas
## Vue-Devtools

https://github.com/vuejs/vue-devtools