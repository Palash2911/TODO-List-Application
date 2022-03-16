<script>
export default{
    name: 'Heads',
    // props: ['title'], - one way
    props: {
        title: String,
    }
    
}
</script>

<template>
    <header>
        <h1>{{ title }}</h1>
    </header>
</template>

<style scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
     }
</style>