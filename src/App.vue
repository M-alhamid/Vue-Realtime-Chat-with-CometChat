<template>
  <div id="app">
    <div v-if="!showChat">
      <p>Demo users: superhero1, superhero2. use only these 2 for demo purposes.</p>
      <p>Username</p>
      <br>
      <input type="text" v-model="username" @keypress.enter="showChat = true" />
      <button @click.prevent="showChat = true">Join Chat</button>
    </div>
    <Chat v-if="showChat" :username="username" />
  </div>
</template>

<script>
import Chat from './components/Chat.vue'

export default {
  name: 'app',
  components: {
    Chat
  },
  data() {
    return {
      username: null,
      showChat: false
    };
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
