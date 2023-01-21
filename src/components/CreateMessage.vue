<template>
    <form @submit="onSubmit" class="createMessage">
        <input type="text" v-model="text" name="text" placeholder="Create Message">
        <input type="submit" value="Send">
    </form>
</template>

<script>

    const today = new Date();
    const hours = today.getHours();
    const minutes = today.getMinutes() < 10 ? `0${today.getMinutes()}` : `${today.getMinutes()}`;
    const AMPM = hours >= 12 ? 'PM' : 'AM';
    const time = `${hours > 12 ? hours - 12 : hours}:${minutes} ${AMPM}`;

    export default {
        name: 'CreateMessage',
        data() {
            return {
                user: '',
                text: '',
                time: time,
            }
        },
        methods: {
            onSubmit(e) {
                e.preventDefault();

                if (!this.text) {
                    return
                }

                const newMessage = {
                    id: Math.floor(Math.random() * 100),
                    user: this.user,
                    text: this.text,
                    time: this.time
                }

                console.log(newMessage);

                this.$emit('create-message', newMessage)

                this.user = ''
                this.text = ''
                this.time = time
            }
        }
    }
</script>

<style scoped>
    .createMessage {
        background-color: var(--medium-green-spring);
    }
</style>