<template>
<div class="pai"  >
  <div class="popup" >
   
  </div>
  <div class="row form z-depth-5" >
    <div class="card" >
        <div class="input-field col s6">
                <input v-model="taskValues.title" id="first_name2" type="text" class="validate">
                <label class="active" for="first_name2">Title</label>
             </div>
             <div class="input-field col s6">
                <input v-model="taskValues.project" id="first_name2" type="text" class="validate">
                <label class="active" for="first_name2">Project</label>
             </div>

             <div class="input-field col s12">
                <input v-model="taskValues.usuario" id="first_name2" type="text" class="validate">
                <label class="active" for="first_name2">Usuario</label>
             </div>

             <button class="col  s5 btn waves-effect waves-light" @click="verificaType"> Confirmar</button>
             <button class="col s5 btn waves-effect  red lighten-1" @click="$emit('closeForm', false)"> Cancelar</button>

    </div>
  </div>
</div>
</template>

<script>
import queries from '@/queries';

export default {
    props: {
        tarefa: Object
    },
    data(){
        return {
            taskValues : {
                id: null,
                project: '',
                usuario: '',
                title: '',
                dueTo: new Date().toLocaleDateString('pt'),
            }
        }

        
    },

    methods : {
        limpaForm () {
            this.taskValues = {
                id: null,
                project: '',
                usuario: '',
                title: '',
                dueTo: new Date().toLocaleDateString('pt'),
            }

        },
        addTask() {
            queries.postTask(this.taskValues, callback => {
                console.log(callback)
                this.$emit('closeForm', false)
                this.limpaForm()
            })
        },
        editaTask() {
            queries.editTask(this.taskValues, callback => {
                this.$emit('closeForm', false)
                this.limpaForm()
                console.log(callback)
            })
        }
    },

    created() {
        this.taskValues = this.tarefa
    },
    computed : {
        verificaType(){
            return this.taskValues.id ? this.editaTask : this.addTask
        }
    }
}
</script>

<style scoped>
   .popup {
    inset: 0;
    opacity: 0.4;
    background-color: rgb(207, 204, 204);
    height: 100vh;
    width: 100%;
    top: 30%;
}
.pai {
    position: absolute;
    height: 100vh;
    display: flex;
    z-index: 10;
    align-items: center;
    justify-content: center;
    top: 0;
    width: 100%;
}

    .form {
        padding: 30px;
        opacity: 1!important;
        position: absolute;
        z-index: 99;
        background-color: white;
        overflow: hidden;
        max-width: 600px;
    }
    button {

        margin-left: 2rem !important;
  
    }
</style>