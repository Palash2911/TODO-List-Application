<template>
    <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
      <div class="text">
        <h3>{{ task.text }}</h3>
        <p>{{ task.day }}</p>
      </div>
        <button @click="$emit('delete-task', task.id)" class="delete">Delete</button>
    </div>
</template>

<script>
    export default{
      name: 'Task',
      props: {
        task: Object,
      },
      // Longer methods
      // methods: {
      //     onDelete(id){
      //       this.$emit('delete-task', id)
      //   }
      // }
    }
</script>

<style scope>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
  display: flex;
  margin-top: 20px;
  justify-content: space-between;
}
.task.reminder {
  border-left: 5px solid green;
}
.delete{
  all: unset;
  width: 60px;
  height: 30px;
  font-size: 14px; 
  font-weight: bold;
  margin-top: 10px;
  border-radius: 10px;
  background-color: #d00000;
  cursor: pointer;
  text-align: center;
  color: white;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>