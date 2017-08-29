# vue-webpack-simple

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

## Algunos cositas del ejemplo
### 1. Bootstrap
Agregué el framework de Twitter colocando la url externa en el index.html:
```
<link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet" type="text/css" />
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
```
### 2. webpack.config.js
Solo agregué el proxy al archivo (dentro del apartado de devServer):
```
proxy: {
  "/api": "desa.midulcedanna.com.ar:8081"
},
host: "0.0.0.0",
port: "8081",
//public: "desa.midulcedanna.com.ar",
inline: true,
  disableHostCheck: true
},
```
### 3. Uso de components y la comunicación entre ellos:
#### 3.1 Estructura de cada componente:
Cada componente debe respetar la siguiente estructura (los css pueden no estar):
```
<template>
.
.
.
Código HTML
.
.
.
</template>

<script type="text/javascript">
.
.
.
Código JS
.
.
.
</script>

<style>
.
.
.
Código CSS
.
.
.
</style>
```
#### 3.2 Importar componentes:
Se importa al componente hijo con la siguiente sintaxis:
```
import componenteHijo from './componenteHijo.vue';
```
Y dentro del objeto 'components':
```
components: {
  componenteHijo,
},
```
### 3.3 Estructura dentro de <script>:
```
<script type="text/javascript">
  export default {
  name: "nombreComponente",
  // Componentes importados
  components: {
    componenteHijo,
  },
  data() {
		return {
      variable1: 'string';
      variable2: true;
      variable3: 5000;
      objeto: [{
  				nombre: 'titulo1',
  				boolean: false,
				}, {
          nombre: 'titulo2',
  				boolean: false,
				}, {
          nombre: 'titulo3',
          boolean: false,
				}, {
          nombre: 'titulo4',
  				boolean: false,
				}],
    },
  methods: {
      metodoUno: function(argumento) {
        código del método 1
      },
      metodoDos: function(argumento) {
        código del método 2
      },
  }
  </script>
```
### 3.4 Comunicación entre componentes -> datos:
Enviarle parámetros a un componente hijo:
- Archivo App.vue:
```
<!-- Envío al componente hijo la 'variable' como 'parámetro'
<tagComponenteHijo ... v-bind:parámetro="variable"></tagComponenteHijo>
.
.
.
<script>
.
.
.
data() {
  return {
    variable: 'string';
  }
}
.
.
.
</script>
```
- Componente hijo:
```
export default {
  name: "nombreComponente",
  props: ['parámetro'], //recibo el parámetro desde el componente padre
  methods: {
    .
    .
    .
  }
  .
  .
  .
  ```
### 3.5 Comunicación entre componentes -> métodos:
Ejecutar un método del componente padre desde el componente hijo:
- Componente padre:
```
<template>
.
.
.
<!-- Mediante v-on: le paso el método del padre y queda escuchando la ejecución del evento para saber cuando ejecutar el método -->
<tagComponenteHijo v-on:metodoEjecutar="metodoComponentePadre"></tagComponenteHijo>
.
.
.
</template>

<script>
.
.
.
methods: {
  // Defino el método a ejecutarse
  metodoComponentePadre: function () {
    Código del método
  }
}
.
.
.
</script>
```
- Componente hijo
```
<template>
  <-- Ejecuto el método del componente hijo -->
  <button type="button"  @click="metodoHijo(parametro)">
</template>

<scrip>
.
.
.
methods: {
  metodoHijo(parametro) {
    // Emito mensaje al componente padre para ejecutar el método
    this.$emit('metodoEjecutar', parametro);
    },
},
.
.
.
</script>
```
### 3.6 Recorrer un objeto:
En el ejemplo se recorre un objeto que tiene varias "tareas". Este objeto se envía desde el componente padre al hijo. Para hacerlo usamos v-for:
```
<!-- Indicamos al <ul> que vamos a recorrer el objeto 'tareas' y que cada elemento será 'tarea'
<ul v-for="tarea in tareas">
  <li>
      .
      .
      .
  </li>
</ul>
```
### 3.7 v-model
Utilizando v-model en un tag de html podemos colocar el valorde una variable utilizada en javascript.
Por ejemplo, si tenemos una variable con nombre variable1 guardada en el data() y la queremos mostrar en el html, utilizamos <input type="text" v-model="this.variable1"/>. Esto nos mostrará dentro de un input text el valor que tiene la variable1. Asimismo, si este input text es editable, a medida que vayamos cambiando el valor mostrado, este también cambiará en la variable javascript.
### 3.8 Diferentes estilos dependiendo de un valor
Podemos establecer un estilo u otro dependiendo de una condición dada. Para ello se utiliza v-bind:class y a continuación entre { } se coloca la condición verdadera y separando por una "," la condición falsa para que muestre una class u la otra.
```
<div v-bind:class="{'tarea tarea-borde-completada' : tarea.done, 'tarea tarea-borde-incompleta' : !tarea.done}">
.
.
.
</div>
