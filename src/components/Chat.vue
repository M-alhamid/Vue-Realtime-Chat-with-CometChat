<template>
    <div>
        <div class="messages-wrapper">
            <h3 v-if="!initialized">Initializing the chat.</h3>
            <p v-if="error">{{ error }}</p>
            <ul>
                <li
                    v-for="(message, index) in messages"
                    :key="index"
                    :class="isMine(message) ? 'right' : 'left'"
                >
                {{message.text}}
                </li>
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
                groupGUID: 'vuegroupchat'
            };
        },
        methods: {
            sendMessage() {
                let messageText = this.newMessage
                let messageType = CometChat.MESSAGE_TYPE.TEXT
                let receiverType = CometChat.RECEIVER_TYPE.GROUP

                let textMessage = new CometChat.TextMessage(this.groupGUID, messageText, messageType, receiverType);

                CometChat.sendMessage(textMessage);
                this.newMessage = ''
            },
            setUserAndListener(user) {
                this.user = user
                let listenerID = "UNIQUE_LISTENER_ID";
                CometChat.addMessageListener(listenerID, new CometChat.MessageListener({
                onTextMessageReceived: message => this.messages.push(message)
                }));
            },
            isMine(message) {
                return message.sender.uid === this.username
            }
        },
        created() {
            let appID = "180d927c69c56";
            let apiKey = "c66c8f9d68f0e14441281e151eb412944c934efc";
            CometChat.init(appID)
                .then(
                () => {
                    this.initialized = true
                    CometChat.login(this.username, apiKey)
                        .then(
                            user => this.setUserAndListener(user),
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
    padding: 0px 0px;
}
.messages-wrapper ul li {
    padding-left: 30px;
    padding-right: 30px;
    margin-bottom: 20px;
    font-weight: bold;
}
.left{
    text-align: left !important;
}

.right{
    text-align: right !important;
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