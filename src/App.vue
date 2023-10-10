<template>
  <IntroToDo/>
  <TaskForm
    @add="addTask"
  />
  <TaskList
    :list="list"
    @delete="deleteTask"
    @completed="completeTask"
    @edit="toggleModalForm"
  />
  <EditModal 
    v-if="toggle" 
    :data="list[indexToEdit]"
    :index="indexToEdit"
    @closed="toggle=false"
    @update="updateTask"
    />
</template>

<script setup>
  import TaskList from './components/TaskList.vue'
  import TaskForm from './components/TaskForm.vue'
  import IntroToDo from "./components/IntroToDo.vue"
  import EditModal from "./components/EditModal.vue"
  import { reactive, ref } from 'vue'
  const list = reactive([
    {
      name: "Do Laundry",
      desc: "Pre wash first, he big meeting",
      status: "pending"
    },
    {
      name: "Play Sport",
      desc: "Go play some football",
      status: "completed"
    },
    {
      name: "Do Homework",
      desc: "BEcause why not",
      status: "completed"
    },
    
  ])
  const toggle = ref(false)
  const indexToEdit = ref(null)

  const deleteTask = (index) =>{
    list.splice(index, 1)
  }
  const completeTask = (params) => {
    const[index, complete] = params
    list[index].status = complete
  }
  const addTask = (nameDesc) => {
    const [name, desc] = nameDesc
    list.unshift({
      name,
      desc,
      status: "pending"
    })
  }
  const toggleModalForm = (indexToggle) => {
    const [index, value] = indexToggle
    toggle.value = value
    indexToEdit.value = index
  }
  const updateTask = (params) =>{
    const [name, desc, index] = params
    const toBeUpdated = list[index]
    toBeUpdated.name = name
    toBeUpdated.desc= desc
  }
</script>
<!-- Same but with options API -->
<!-- 
  <script>
import TaskList from './components/TaskList.vue'
import TaskForm from './components/TaskForm.vue'
import IntroToDo from "./components/IntroToDo.vue"
import EditModal from "./components/EditModal.vue"

export default {
  name: 'App',
  components: {
    TaskList,
    TaskForm,
    IntroToDo,
    EditModal
  },
  data(){
    return {
      list: [
        {
          name: "Do Laundry",
          desc: "Pre wash first, he big meeting",
          status: "pending"
        },
        {
          name: "Play Sport",
          desc: "Go play some football",
          status: "completed"
        },
        {
          name: "Do Homewrok",
          desc: "BEcause why not",
          status: "pending"
        },
        
      ],
      toggle: false,
      indexToEdit: null
    }
  },
  methods: {
    deleteTask(index){
      this.list.splice(index, 1)
    },
    completeTask(params){
      const[index, complete] = params
      if(complete){
        this.list[index].status = "completed"
      }else {
        this.list[index].status = "pending"
      }
    },
    addTask(nameDesc){
      const [name, desc] = nameDesc
      this.list.unshift({
        name,
        desc,
        status: "pending"
      })
    },
    toggleModalForm(indexToggle){
      const [index, value] = indexToggle
      this.toggle = value
      this.indexToEdit = index
    },
    updateTask(params){
      const [name, desc, index] = params
      const toBeUpdated = this.list[index]
      toBeUpdated.name = name
      toBeUpdated.desc= desc
    }
  }
}
</script>
 -->

<style>
  body {
    background-color: rgb(238, 238, 238);
  }
</style>
