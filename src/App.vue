<template>
  <div class="container">
    <Header title="Ping" @set-username="setUsername"/>
    <Messages :messages="messages"/>
    <CreateMessage :messages="messages" @create-message="createMessage"/>
  </div>
</template>

<script>
  import CreateMessage from './components/CreateMessage.vue';
  import Header from './components/Header.vue';
  import Messages from './components/Messages.vue';

  import { initializeApp } from "firebase/app";
  import { collection, getDocs, getFirestore, 
    onSnapshot, addDoc, query, 
    orderBy, setDoc, doc} from "firebase/firestore";

  import { v4 as uuidv4 } from 'uuid';

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
      setUsername(username) {
        this.username = username;
      },
      async createMessage(message) {
        await addDoc(collection(db, "messages"), {
          uuid: this.getUuid(),
          username: this.username,
          messageText: message.messageText,
          timeText: message.timeText,
          timeStamp: message.timeStamp,
        });
      },
      async createUuid(uuidReference) {
        addDoc(uuidReference, localStorageGet, {
          uuid: localStorageGet
        });
      },
      getUuid() {
        return localStorage.getItem("uuid");
      }
    },
    data() {
      return {
        uuid: '',
        username: '',
        messages: [],
      }
    },
    created() {
      this.uuid = ''
      this.username = 'Anonymous'
      this.messages = []
    },
    async mounted() {
      const localStorageGet = localStorage.getItem("uuid");
      if (!localStorageGet) {
        localStorage.setItem("uuid", uuidv4());
      }

      const uuidReference = collection(db, "uuid");
      const uuidSnapshot = await getDocs(uuidReference);

      const filter = uuidSnapshot.docs.filter(doc => doc.uuid != localStorageGet);
      if (uuidSnapshot.docs.length != 0) {
        uuidSnapshot.forEach(doc => {
          console.log(doc.data().uuid);
          console.log(filter);
          if (filter.length <= 0) {
            this.uuid = localStorageGet;
            this.createUuid(uuidReference, localStorageGet);
            return;
          }
        });
      } else {
        this.uuid = localStorageGet;
        this.createUuid(uuidReference);
        return;
      }
      

      const newQuery = query(collection(db, "messages"), orderBy("timeStamp"));
      onSnapshot(newQuery, (querySnapshot) => {
        const fbMessages = [];
        querySnapshot.forEach((doc) => {
          const message = {
            username: doc.data().username,
            messageText: doc.data().messageText,
            timeText: doc.data().timeText,
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

    body, html {
      display: inline-flex;
      height: 100vh;
      width: 100vw;
      margin: 0;
      padding: 0;
      background-color: var(--dark-jungle-green);
      justify-content: center;
      align-items: center;
      /* overflow: hidden; */
    } 
    
    .container {
      margin: 2.5vw 2.5vh;
      display: inline-flex;
      flex-direction: column;
      width: 90vw;
    }

    svg {
      width: 0;
      height: 0;
    }
</style>
