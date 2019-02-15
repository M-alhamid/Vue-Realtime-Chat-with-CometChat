<template>
    <div>
        <div class="messages-wrapper">
            <ul>
                <li v-for="(message, index) in messages" :key="index"> {{message}} </li>
            </ul>
        </div>
        <p>Your message goes here</p>
        <div class="input-wrapper">
            <input type="text" class="message-text" v-model="newMessage" @keypress.enter="sendMessage">
            <button class="new-message" @click="sendMessage">Send Message</button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                newMessage: '',
                messages: []
            };
        },
        methods: {
            sendMessage() {
                this.messages.push(this.newMessage)
                this.newMessage = ''
            }
        }
    }
</script>

<style scoped>
.messages-wrapper{
    width: 800px;
    height: 500px;
    background: pink;
    margin:auto;
    overflow-y: scroll;
}
.messages-wrapper ul {
    list-style: none;
}
.messages-wrapper ul li {
    padding: 20px 10px;
}
.messages-wrapper ul li .left{
    text-align: left;
}

.messages-wrapper ul li .right{
    text-align: right;
}
.input-wrapper {
    width: 800px;
    height: 40px;
    margin: auto;
}
.message-text {
    width: 80%;
    height: inherit;
}
.new-message {
    width: 15%;
    height: inherit;
    margin-left: 20px;
}
</style>