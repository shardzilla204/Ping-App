<template>
    <header>
        <!-- <svg class="back">
            <use href="#arrow"/>
        </svg> -->
        <h1>{{ name }}</h1>
        <CreateUsername @set-username="setUsername"/>
    </header>
</template>

<script>
import CreateUsername from './CreateUsername.vue';

export default {
    name: "Header",
    props: {
        name: String,
    },
    components: { 
        CreateUsername,
    },
    data() {
        return {
            username: '',
        }
    },
    methods: {
        setUsername(name) {
            this.username = name;
            this.$emit('set-username', this.username);

            if (this.username.length > 0 && this.username.trim() != '') return;

            this.username = 'Anonymous';
            this.$emit('set-username', this.username);

        }
    },
}
</script>

<style scoped>
    header {
        background-color: #D8E4FF;
        display: flex;
        align-items: center;
        border-radius: 15px 15px 0px 0px;
        z-index: 1;
        grid-area: "header";
    }

    h1 {
        flex: 2;
        text-align: center;
        color: #6B818C;
    }

    .back {
        padding: 15px;
        transform: rotatez(-90deg);
        fill: #6B818C;
        width: 50px;
        height: 50px;
    }
    .back:active {
        filter: brightness(1.25);
    }
</style>
