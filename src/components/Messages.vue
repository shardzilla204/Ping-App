<template>
    <section class="messages">
        <div class="messagesContainer">
            <div class="messageContainer" :key="message.id" v-for="message in messages">
                <Message :message="message"/> 
            </div>
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
    },
    methods: {
        createMessage(message) {
            this.messages = [...this.messages, message]
            document.getElementsByClassName(messagesContainer).style.backgroundColor = "blue";
        },
    },
}
</script>

<style scoped>
    .messages {
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
        align-items: flex-end;
        padding: 0vw 2.5vh 0vw 2.5vh;
        background-color: #C2CDE5;
        max-height: 70vh;
        min-height: 65vh;
    }

    .messagesContainer {
        padding: 25px 0px 25px 0px;
        overflow: auto;
    }

    .messagesContainer::-webkit-scrollbar {
        width: 0px;
    }
</style>