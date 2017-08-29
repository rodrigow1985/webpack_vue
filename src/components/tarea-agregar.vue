<template>
  <div>
    <!-- Trigger the modal with a button -->
    <button type="button" class="btn btn-info btn-lg" data-toggle="modal" data-target="#myModal" title="Agregar">
      <span class="glyphicon glyphicon-plus"></span>
    </button>

    <!-- Modal -->
    <div id="myModal" class="modal fade" role="dialog">
      <div class="modal-dialog">
        <!-- Modal content-->
        <div class="modal-content">
          <!-- Header del modal -->
          <div class="modal-header">
            <button type="button" class="close" data-dismiss="modal" @click="limpiarNuevaTarea()">&times;</button>
            <h4 class="modal-title">Agregar tarea</h4>
          </div>
          <!-- Cuerpo del modal -->
          <div class="modal-body"style="text-align: left">
            <label for="nuevaTarea">Tarea</label>
            <input type="text" class="form-control" placeholder="Ingrese una nueva tarea" v-model="nuevaTarea"/>

            <label for="nuevaTareaProyecto">Proyecto</label>
            <input type="text" class="form-control" placeholder="Ingrese el proyecto de la tarea" v-model="nuevaTareaProyecto"/>
          </div>
          <!-- Botón cerrar -->
          <div class="modal-footer">
            <button type="button" class="btn btn-default" data-dismiss="modal" @click="agregarTarea(nuevaTarea, nuevaTareaProyecto)">
              <span class="glyphicon glyphicon-plus"></span>
              Agregar
            </button>
            <button type="button" class="btn btn-default" data-dismiss="modal" @click="limpiarNuevaTarea()">
              <span class="glyphicon glyphicon-remove"></span>
              Cancelar
            </button>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script type="text/javascript">

  export default {
    name: "tareaAgregar",
    data() {
      return {
        nuevaTarea: '',
        nuevaTareaProyecto: '',
      }
    },
    methods: {
      agregarTarea(nuevaTarea, nuevaTareaProyecto) {
        this.$emit('agregarTarea', nuevaTarea, nuevaTareaProyecto); // Emito mensaje al componente padre para que me agregue la tarea ingresada
        this.limpiarNuevaTarea();
        },
      limpiarNuevaTarea: function() {
        this.nuevaTarea='';
        this.nuevaTareaProyecto='';
      }
    },
  }

</script>
