<template>
    <form @submit="onSubmit" class="createMessage">
        <input class="message" type="text" v-model="text" name="text" placeholder="Message...">
        <!-- <img v-on:click="onSubmit" class="submit" src="../assets/arrow.svg"> -->
        <svg viewBox="-100 -65 575 575" class="submit" @click="onSubmit">
            <g class="arrow">
                <path d="M 185.34375 0.43554688 A 17.473618 19.89225 0 0 0 173.84375 9.9453125 L 72.958984 208.86914 L 2.3417969 348.11523 A 17.473618 19.89225 0 0 0 17.472656 377.95312 L 165.35352 377.95312 L 165.35352 214.74609 C 165.35352 200.46979 175.88995 188.97656 188.97656 188.97656 C 202.06318 188.97656 212.59766 200.46979 212.59766 214.74609 L 212.59766 377.95312 L 219.24219 377.95312 L 360.47852 377.95312 A 17.473618 19.89225 0 0 0 375.61133 348.11523 L 274.72852 149.19141 L 204.10938 9.9453125 A 17.473618 19.89225 0 0 0 185.34375 0.43554688 z" transform="scale(1)"/>
            </g>
        </svg>
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
        padding: 15px;
        display: flex;
        border-radius: 0px 0px 15px 15px;
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