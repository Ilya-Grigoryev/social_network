<template>
<div>
    <v-row><v-col cols="10">
        <div class="container">
            <ChatWindow v-on:send-message="sendMessage" permanent>
                <ChatMessage v-for="(message, key) in messages" :key="key" 
                                            :username="message.author" 
                                            :datetime="message.datetime">
                        <div class="message">{{message.text}}</div>
                </ChatMessage>
            </ChatWindow>
        </div>
    </v-col></v-row>
</div>
</template>

<script>

import ChatWindow from '@/components/ChatWindow.vue'
import ChatMessage from '@/components/ChatMessage.vue'

export default {
    components: {
        ChatWindow,
        ChatMessage,
    },
    props:['user', 'myId'],
    data(){
    return{
        messages: [],
    }},
    methods: {
        getMessage(){
        this.axios.get('http://188.225.47.187/api/jsonstorage/8572996d89410a6488472c0ae6dfbf34')
        .then((response) => {
            this.messages = response.data
        })
        },
        sendMessage(newMess){ if (newMess != '') {

            let t = new Date()

            this.messages.push({
                id: this.myId,
                author: this.user.name,
                text: newMess,
                datetime: t.getUTCDate() +"."+ String(Number(t.getMonth())+1) +"."+ t.getFullYear() +" "+ t.getHours() +":"+ t.getMinutes() +":"+ t.getSeconds()
            })

            this.axios.put('http://188.225.47.187/api/jsonstorage/8572996d89410a6488472c0ae6dfbf34', this.messages)
            .then(()=>{
                this.getMessage();
            })
        }}
    },
    mounted(){
        this.getMessage();

        setInterval(() => this.getMessage(), 100);
    },
    watch:{
        $route(){
            this.getMessage();
        }
    },
}
</script>


<style scoped>

.container {
    text-align: left;
    margin: auto;
    box-shadow: 0 0 15px 0 #5f5f5f73;
}

</style>