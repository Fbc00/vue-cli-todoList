<template>
  <div class="hello centraliza">
    <div class="container ">
    <div class="col s12 m6 " v-for="tarefa in tasks" :key="tarefa.id">
      <div class=" card blue-grey darken-1">
        <div class="card-content white-text">
          <span class="card-title">  {{ tarefa.title }}</span>
          <p>
            {{ tarefa.project }}
          </p>
          <p> {{ tarefa.usuario}}</p>
        </div>
        <div class="card-action">
          <button
          class=" btn-large waves-effect  red"
          @click="deletarTask(tarefa)"> Excluir </button>
          <button  class=" btn-large waves-effect waves-light " @click="EditarTask(tarefa)"> Editar </button>
        </div>
      </div>
    </div>
  </div>
</div>
</template>
<script>
import queries from '../queries'

export default {
  name: 'HelloWorld',
  props: {
    tasks: Array
  },
  methods : {
    deletarTask(tarefa){
      queries.deleteTask(tarefa, callback=> {
          console.log('task deletada ', callback)
      })
    },
    EditarTask(tarefa) {
     this.$emit('editaAi', {formMostra: true, taskForm:tarefa})
    }
   }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  button {
    margin-left: 2rem !important;
  }
</style>
