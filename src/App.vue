<template>
  <div id="app">
    <tareaList v-bind:tareas="tareas"></tareaList>
    <tareaAgregar v-on:agregarTarea="agregarTarea"></tareaAgregar>
    <pre>
    	{{ $data || json }}
    </pre>
  </div>
</template>

<script>
import tareaList from './components/tarea-list.vue';
import tareaAgregar from './components/tarea-agregar.vue';

export default {
  name: 'app',

  components: {
    tareaList,
    tareaAgregar,
  },

	data() {
		return {
      // Defino un objeto con tareas
			tareas: [{
				nombre: 'Todo A',
				project: 'Project A',
				done: false,
				}, {
				nombre: 'Todo B',
				project: 'Project B',
				done: true,
				}, {
				nombre: 'Todo C',
				project: 'Project C',
				done: false,
				}, {
				nombre: 'Todo D',
				project: 'Project D',
				done: false,
				}],
		};
	},
		methods: {
      agregarTarea: function(tarea, proyecto) {
  			if(tarea.trim() || proyecto.trim()) { //Pregunto si lo ingresado es vacío
              	this.tareas.push({nombre: tarea, project: proyecto, done: false}) //Agrego tarea al objeto tareas
              	} else {
                  alert('Debe introducir un nombre para la tarea y/o proyecto')
                  }
  			},
    },
  };
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

/*a {
  color: #73AD21;
}*/

.tarea {
	text-align: left;
    border-radius: 25px;
    padding: 15px;
    width: 350px;
}

.tarea-borde-completada {
  border: 1px solid #73AD21;
}

.tarea-borde-incompleta {
  border: 1px solid #F6CECE;
}

.tarea-nombre {
	font-weight: bold;
}

.tarea-proyecto{
  color: grey;
}

.tarea-botonera {
	text-align: right;
  margin-bottom: 17px;
}

.tarea-done {
  text-align: center;
  margin:-17px;
  border-bottom-left-radius: 25px;
  border-bottom-right-radius: 25px;
  /*border: 2px solid #73AD21;*/
  height: 30px;
  padding: 4px;
}
</style>
