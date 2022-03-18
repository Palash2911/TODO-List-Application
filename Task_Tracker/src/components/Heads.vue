<script>
import Button from './Button.vue'
export default{
    name: 'Heads',
    // props: ['title'], - one way
    props: {
        title: String,
        showAddTask: Boolean,
    },
    components: {
        Button
    }
}
</script>

<template>
    <header>
        <h1>{{ title }}</h1>
        <Button @show-add-task="$emit('showadd-task')" :text="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'red' : 'green'" />
    </header>
</template>

<style scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
     }
</style>