<template>
    <header>
        <h1>{{ title }}</h1>
    </header>
</template>

<script>
export default {
    name: 'Header',
    props: {
        title: String,
    }
}
</script>

<style scoped>
    header {
        height: 10vh;
        background-color: #D8E4FF;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    h1 {
        color: #6B818C;
    }
</style>
