<template>
    <form @submit="onSubmit" class="createMessage">
        <input class="message" type="text" v-model="messageText" name="messageText" placeholder="Message..." autocomplete="off">
        <!-- <img v-on:click="onSubmit" class="submit" src="../assets/arrow.svg"> -->
        <svg class="submit" @click="onSubmit">
            <use href="#arrow"/>
        </svg>
    </form>
</template>

<script>
    import { serverTimestamp } from '@firebase/firestore';
    export default {
        name: 'CreateMessage',
        props: {
            messages: Array,
        },
        data() {
            return {
                username: '',
                messageText: '',
            }
        },
        methods: {
            onSubmit(e) {
                const timeString = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })

                e.preventDefault();

                if (!this.messageText) {
                    return;
                }

                const newMessage = {
                    username: this.username,
                    messageText: this.messageText,
                    timeText: timeString,
                    timeStamp: serverTimestamp()
                }

                this.$emit('create-message', newMessage)

                this.username = ''
                this.messageText = ''
                this.timeText = timeString
                this.timeStamp = serverTimestamp();
            }
        },
    }
</script>

<style scoped>
    .createMessage {
        background-color: var(--medium-green-spring);
        padding: 15px;
        display: flex;
        border-radius: 0px 0px 15px 15px;
        z-index: 1;
        grid-area: "createMessage";
    }

    .message {
        flex-grow: 1;
        background-color: #2BCF72;
        border: none;
        border-radius: 15px;
        outline-style: none;
        padding: 15px;
        margin-right: 15px;
        color: #FFFFFF;
        min-height: 20px;
    }

    .submit {
        background-color: var(--lavender-web);
        border: none;
        border-radius: 50px;
        outline-style: none;
        width: 50px;
        height: 50px;
        fill: #C2CDE5;
    }

    .submit:active {
        filter: brightness(0.95);
    }
</style>