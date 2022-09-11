<template>
  <div id="app">
    <div class="main">
          <TaskComponente  
          :tasks="tasks"
          @editaAi="formEdit"
          />
          <button 
          @click="addTask" 
          class="btn-floating btn-large waves-effect waves-light red"><i class="fa-solid fa-plus"></i></button >
          <FormTask v-if="formMostra" @closeForm="formMostra = $event" :tarefa="taskForm" />
    </div>
  </div>
</template>

<script>

import TaskComponente from './components/taskComponente.vue'
import queries from './queries'
import FormTask from './components/formTask.vue'


export default {
  name: 'App',
  components: {
    TaskComponente,
    FormTask
},
  data () {
    return {
      formMostra: false,
      tasks: [],
      taskForm: {
                id: null,
                project: '',
                usuario: '',
                title: '',
                dueTo: new Date().toLocaleDateString('pt'),
            }
    }
  },

  methods: {
    addTask () {
      this.formMostra = true
    },
    formEdit(evento){
      this.taskForm = evento.taskForm
      this.formMostra = evento.formMostra
    }
  },
  created() {
    queries.getTasks(callback => {
      this.tasks = callback
    })
    }
}
</script>

<style>
.container {
  position: relative;
}
#app {
  
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>


