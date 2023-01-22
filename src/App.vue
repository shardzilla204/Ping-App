<template>
  <Header title="Ping"/>
  <Messages :messages="messages"/>
  <CreateMessage @create-message="createMessage"/>
</template>

<script>
  import CreateMessage from './components/CreateMessage.vue';
  import Header from './components/Header.vue';
  import Messages from './components/Messages.vue';
  // import db from './firebase/index.js'

  import { initializeApp } from "firebase/app";
  import { collection, getDocs, getFirestore, onSnapshot, addDoc } from "firebase/firestore";

  const firebaseConfig = {
    apiKey: "AIzaSyDqnmbXypz1C_I7TKGVfm-R1xqshWJSm6s",
    authDomain: "ping-eea8c.firebaseapp.com",
    projectId: "ping-eea8c",
    storageBucket: "ping-eea8c.appspot.com",
    messagingSenderId: "787406763082",
    appId: "1:787406763082:web:db19e31e34eddb498da2b3",
    measurementId: "G-SWXN5ZEFPF"
  };

  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);


  export default {
    name: 'App',
    components: {
    Header,
    Messages,
    CreateMessage
},
    methods: {
      async createMessage(message) {
        await addDoc(collection(db, "messages"), {
          user: message.user,
          text: message.text,
          time: message.time
        });
      },
    },
    data() {
      return {
        messages: []
      }
    },
    created() {
      this.messages = []
    },
    mounted() {
      onSnapshot(collection(db, "messages"), (querySnapshot) => {
        const fbMessages = [];
        querySnapshot.forEach((doc) => {
          console.log(doc.id, " => ", doc.data());
          const message = {
            id: doc.id, 
            user: doc.data().user,
            text: doc.data().text,
            time: doc.data().time,
          }
          fbMessages.push(message)
        });
        this.messages = fbMessages;
      });
      
    },
  }
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Nunito&display=swap');
    :root {
      font-family: 'Nunito', sans-serif;
      --dark-jungle-green: #00120B;
      --dark-slate-gray: #35605A;
      --slate-gray: #6B818C;
      --lavender-web: #D8E4FF;
      --medium-green-spring: #31E981;
    }

    ::placeholder {
        color: #FFFFFF;
        font-family: 'Nunito', sans-serif;
    }

    body {
      margin: 0;
      background-color: var(--dark-jungle-green);  
    } 
</style>
