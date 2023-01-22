<template>
    <section class="messagesContainer">
        <div :key="message.id" v-for="message in messages">
            <Message :message="message"/>
        </div>
    </section>
</template>

<script>
import Message from './Message.vue'
    
export default {
    name: 'Messages',
    props: {
        messages: Array,
    },
    components: {
    Message,
    methods: {
        createMessage(message) {
            this.messages = [...this.messages, message]
        },
    }
},
}
</script>

<style scoped>
    .messagesContainer {
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        align-items: flex-end;
        gap: 25px;
        padding: 25px 15px 25px 15px;
        background-color: #C2CDE5;
        flex: 1 1 auto;
    }
</style>