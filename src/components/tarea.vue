<template>

  <div v-bind:class="{'tarea tarea-borde-completada' : tarea.done, 'tarea tarea-borde-incompleta' : !tarea.done}">
    <!-- Si no es editable -->
    <div class="tarea-nombre" v-show="!this.editar">{{ tarea.nombre }}</div>
    <div class="tarea-proyecto" v-show="!this.editar"><h5>{{ tarea.project}}</h5></div>
    <!-- Si es editable -->
    <form class="md-form" style="margin: 5px">
      <div class="md-form"  v-show="this.editar" v-model="tarea.nombre">
        <input type="text"
          class="tarea-nombre"
          id="editarNombre"
          style="border: 0; outline: 0; background: transparent; border-bottom: 1px solid grey;"
          v-model="nuevoNombre"
          >
        <input type="text"
          class="tarea-proyecto"
          id="editarProject"
          style="border: 0; outline: 0; background: transparent; border-bottom: 1px solid grey;"
          v-model="nuevoProject"
          >
        </div>
    </form>
    <div class="tarea-botonera">
      <a href="#" @click="completarTarea(tarea)" v-show="!tarea.done && !this.editar">
        <span class="glyphicon glyphicon-check" title="Completar"></span>
      </a>
      <a href="#" @click="editarHandler()" v-show="!this.editar">
        <span class="glyphicon glyphicon-edit" title="Editar"></span>
      </a>
      <a href="#" @click="tareaActualizar()" v-show="this.editar">
        <span class="glyphicon glyphicon-save" title="Guardar"></span>
      </a>
      <a href="#" @click="eliminarTarea(tarea)" v-show="!this.editar">
        <span class="glyphicon glyphicon-trash" title="Eliminar"></span>
      </a>
    </div>
    <!-- Tarea completada o incompleta -->
    <div class="tarea-done alert alert-success" v-show="tarea.done" disabled>Completada</div>
    <div class="tarea-done alert alert-danger" v-show="!tarea.done">Incompleta</div>
  </div>

</template>

<script type="text/javascript">

export default {
  name: 'tarea',
  props: ['tarea', 'colores'],
  data() {
		return {
      nuevoNombre: this.tarea.nombre,
      nuevoProject: this.tarea.project,
      editar: false,
    }
  },
  methods: {
    editarHandler() {
      this.editar = !this.editar;
    },
    tareaActualizar() {
      this.editarHandler();
      this.$emit('tareaActualizar', this.tarea, this.nuevoNombre, this.nuevoProject);
    },
    completarTarea(tarea) {
      this.$emit('completarTarea', tarea);
    },
    eliminarTarea(tarea) {
        this.$emit('eliminarTarea', tarea);
      },
  }

}

</script>
