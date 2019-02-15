<template>
    <div>
        <div class="messages-wrapper">

        </div>
        <p>Your message goes here</p>
        <div class="input-wrapper">
            <input type="text" class="message-text">
            <button class="new-message">Send Message</button>
        </div>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style scoped>
.messages-wrapper{
    width: 800px;
    height: 500px;
    background: pink;
    margin:auto;
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