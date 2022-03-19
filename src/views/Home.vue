<template>
     <div v-show="showAddTask">
        <AddTask @add-task="addTask"/> 
     </div>
     <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
</template>

<script>
    import Tasks from '../components/Tasks.vue'
    import AddTask from '../components/AddTask.vue'

    export default{
        name: 'Home',
        props: {
            showAddTask: Boolean,
        },
        components: {
            Tasks,
            AddTask,
        },
        data() {
            return{
                tasks: [],
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