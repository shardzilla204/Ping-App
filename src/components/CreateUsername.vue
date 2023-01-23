<template>
    <input class="username" type="text" v-model="username" @input="setUsername" placeholder="Username..." autocomplete="off">
</template>
<script>
    export default {
        name: 'CreateUsername',
        data() {
            return {
                username: '',
            }
        },
        methods: {
            setUsername() {
                this.$emit('set-username', this.username);
            },
        }
    }
</script>

<style scoped>
    .username {
        flex-grow: 1;
        max-width: 20%;
        background-color: #C2CDE5;
        border: none;
        border-radius: 15px;
        outline-style: none;
        padding: 15px;
        margin-right: 15px;
        color: #FFFFFF;
        min-height: 20px;
    }
</style>