<template>
    <div>
        <div class="messages-wrapper">
            <h3 v-if="!initialized">Initializing the chat.</h3>
            <p v-if="error">{{ error }}</p>
            <ul v-else>
                <li v-for="(message, index) in messages" :key="index"> {{message}} </li>
            </ul>
        </div>
        <div v-if="initialized">
            <p>Your message goes here</p>
            <div class="input-wrapper">
                <input type="text" class="message-text" v-model="newMessage" @keypress.enter="sendMessage">
                <button class="new-message" @click="sendMessage">Send Message</button>
            </div>
        </div>
    </div>
</template>

<script>
import { CometChat } from '@cometchat-pro/chat/CometChat.js'
    export default {
        props: {
            username: {
                type: String,
                required: true,
            }
        },
        data() {
            return {
                newMessage: '',
                messages: [],
                initialized: false,
                error: null,
                user: null,
            };
        },
        methods: {
            sendMessage() {
                this.messages.push(this.newMessage)
                this.newMessage = ''
            }
        },
        created() {
            var appID = "180d927c69c56";
            var apiKey = "c66c8f9d68f0e14441281e151eb412944c934efc";
            CometChat.init(appID)
                .then(
                () => {
                    this.initialized = true
                    CometChat.login(this.username, apiKey)
                        .then(
                            user => this.user = user,
                            error => this.error = error
                        );
                },
                error => this.error = error
                );
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