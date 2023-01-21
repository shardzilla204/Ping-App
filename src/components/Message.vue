<template>
    <div class="messageContainer">
        <!-- <div class="user">{{ message.user }}</div> -->
        <div class="message">{{ message.text }}</div>
        <div class="time">Sent {{ message.time }}</div>
    </div>
</template>

<script>
export default {
    name: 'Message',
    props: {
        message: Object,
    },
}
</script>

<style scoped>
    .messageContainer {
        display: flex;
        flex-direction: column;
        align-items: end;
        gap: 5px;
    }
    .user {
        color: var(--slate-gray);
        font-size: 10px;
    }
    .message {
        background-color: var(--slate-gray);
        color: #FFFFFF;
        padding: 10px;
        border-radius: 15px 15px 0px 15px;
        max-width: 12.5em;
    }
    .time {
        color: var(--slate-gray);
        font-size: 10px;
        font-weight: 1000;
    }
</style>