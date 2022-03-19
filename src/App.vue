<script>
import Heads from './components/Heads.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default{
    name: 'App',
    components: {
        Heads,
        Tasks,
        AddTask,

    },
    data(){
      return {
         tasks: [],
         showAddTask: false,
      }
    },
    methods:{
        async addTask(task){

          const res = await fetch('http://localhost:5000/tasks', {
            method: 'POST',
            headers: {
              'Content-type' : 'application/json',
            },
            body: JSON.stringify(task)
          })

          const data = await res.json()

          this.tasks = [...this.tasks, task]
        },
        async toggleReminder(id){
          const tasktotoggle = await this.fetchTask(id)
          const updTask = {...tasktotoggle, reminder: !tasktotoggle.reminder}

          const res = await fetch(`http://localhost:5000/tasks/${id}`, {
            method: 'PUT',
            headers: {
              'Content-type': 'application/json',
            },
            body: JSON.stringify(updTask),
          })

            const data = await res.json()

            this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder} : task
            )
        },
        async deleteTask(id)
        {
          if(confirm('You Sure ?'))
          {
            const res = await fetch(`http://localhost:5000/tasks/${id}`, {
              method: 'DELETE',
            })

            res.status()==200 ? (this.tasks = this.tasks.filter((task) => task.id!==id)) : alert('Error Deleting Task !!')
            
          }
        },
        showAdd()
        {
          this.showAddTask = !this.showAddTask
        },
        async fetchtask()
        {
            const res = await fetch('http://localhost:5000/tasks')
            
            const data = await res.json()

            return data
        },
        async fetchTask(id)
        {
            const res = await fetch(`http://localhost:5000/tasks/${id}`)
            
            const data = await res.json()

            return data
        },
    },
    async created() {
        this.tasks = await this.fetchtask()
    }
}
</script>


<template>
  <header>
    <div class="container"> 
     <Heads @showadd-task="showAdd()" title="Palash" :showAddTask="showAddTask"/>
     <div v-show="showAddTask">
        <AddTask @add-task="addTask"/> 
     </div>
     <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
    </div>
  </header>
</template>


<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: 'Poppins', sans-serif;
  }
  .container {
    max-width: 500px;
    margin: 30px auto;
    overflow: auto;
    min-height: 300px;
    border: 1px solid steelblue;
    padding: 30px;
    border-radius: 5px;
  }
  .btn {
    display: inline-block;
    background: #000;
    color: #fff;
    border: none;
    padding: 10px 20px;
    margin: 5px;
    border-radius: 5px;
    cursor: pointer;
    text-decoration: none;
    font-size: 15px;
    font-family: inherit;
  }
  .btn:focus {
    outline: none;
  }
  .btn:active {
    transform: scale(0.98);
  }
  .btn-block {
    display: block;
    width: 100%;
  }

</style>
