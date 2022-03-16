<script>
import Heads from './components/Heads.vue'
import Tasks from './components/Tasks.vue'

export default{
    name: 'App',
    components: {
        Heads,
        Tasks
    },
    data(){
      return {
         tasks: []
      }
    },
    created() {
        this.tasks = [
            {
                id: 1,
                text: "You Can Do it",
                day: "March 1st at 1:00pm",
                reminder: true,
            },
            {
                id: 2,
                text: "Wake Up",
                day: "March 31st at 5:00pm",
                reminder: false,
            },
            {
                id: 3,
                text: "Sleep",
                day: "April 1st at 7:00pm",
                reminder: true,
            },
        ]
    }
}
</script>


<template>
  <header>
    <div class="container"> 
     <Heads title="Palash"/>
     <Tasks :tasks="tasks"/>
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
