<script>
import Button from './Button.vue'
export default{
    name: 'Heads',
    // props: ['title'], - one way
    props: {
        title: String,
    },
    components: {
        Button
    }
}
</script>

<template>
    <header>
        <h1>{{ title }}</h1>

        <Button text="Add Task" color="Green" />
    </header>
</template>

<style scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
     }
</style>