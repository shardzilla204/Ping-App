<template>
    <div class="information">
        <div class="username">{{ message.username }}</div>
        <div class="message">{{ message.messageText }}</div>
        <div class="timeText">Sent {{ message.timeText }}</div>
    </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';
export default {
    name: 'Message',
    props: {
        message: Object,
        timeStamp: String,
    },
    methods: {
        onClick() {
            console.log(uuidv4());
        }
    }
}
</script>

<style scoped>
    .information {
        display: flex;
        flex-direction: column;
        align-items: end;
        gap: 5px; 
    }

    .username {
        color: var(--slate-gray);
        font-size: 15px;
    }

    .message {
        background-color: var(--slate-gray);
        color: #FFFFFF;
        padding: 10px;
        padding-right: 20px;
        border-radius: 15px 15px 0px 15px;
        max-width: 50%;
    }

    .message:hover {
        background-color: black;
    }
    
    .timeText {
        color: var(--slate-gray);
        font-size: 10px;
        font-weight: 1000;
    }
</style>