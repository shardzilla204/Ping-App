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
        min-height: 100px;
        background-color: #D8E4FF;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 15px 15px 0px 0px;
    }

    h1 {
        color: #6B818C;
    }
</style>
