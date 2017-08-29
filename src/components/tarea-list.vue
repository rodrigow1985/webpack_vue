<template>
  <div>
    <!-- Filtros -->
    <div class="btn-group">
      <button type="button" class="btn btn-default btn-filter" @click="valorFiltro(null)">Todos</button>
			<button type="button" class="btn btn-success btn-filter" @click="valorFiltro(true)">Completadas</button>
			<button type="button" class="btn btn-danger btn-filter" @click="valorFiltro(false)">Incompletas</button>
		</div><br/>
  </br/>
    <!-- Recorro el objeto tareas -->
    <ul v-for="tarea in tareasFiltradas">
      <li>
        <tarea v-on:eliminarTarea="eliminarTarea"
          v-on:completarTarea="completarTarea"
          v-on:tareaActualizar="tareaActualizar"
          v-bind:tarea="tarea"></tarea>
      </li>
    </ul>
  </div>


</template>

<script type="text/javascript">
import tarea from './tarea.vue';

export default {
  name: "tareaList",
  props: ['tareas'],
  components: {
    tarea,
  },
  data() {
    return {
      filtroValor: null,
    }
  },
  methods: {
    tareaActualizar: function(tarea, nuevoNombre, nuevoProject) {
      const tareaIndex = this.tareas.indexOf(tarea);
      this.tareas[tareaIndex].nombre = nuevoNombre;
      this.tareas[tareaIndex].project = nuevoProject;
    },
    completarTarea: function (tarea) {
      const tareaIndex = this.tareas.indexOf(tarea);
      this.tareas[tareaIndex].done = true;
    },
  	eliminarTarea: function(tarea) {
    	if(confirm('¿Eliminar ' + tarea.nombre + '?'))
        	this.tareas.splice(this.tareas.indexOf(tarea), 1)
        },
    valorFiltro: function(valor) {
      this.filtroValor = valor;
    },
  },
  computed: {
    tareasFiltradas: function () {
      if(this.filtroValor==null) {
        return this.tareas;
      } else {
        return this.tareas.filter(function (tarea) {
          return tarea.done == this.filtroValor;
        }.bind(this))//Para poder usar this.filtroValor le tuve que agregar el .bind(this)
      }
    },
  }
}
</script>
