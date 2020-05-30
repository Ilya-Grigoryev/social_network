<template>
    <div :v-if="profile!== null">
        <v-row class="text-left">
            <v-col cols="10">
                <h1 class="text--darken-2">
                    <div style="color: #5A009D;">
                        <v-icon large color="#5A009D">mdi-account-outline</v-icon>
                        {{profile.name}}
                    </div>
                </h1>
            </v-col>
        </v-row>
        


        <div style="text-align: left;" v-if="this.$route.params.id == myId">
            <v-col cols="10">
            <v-card outlined max-width="1000" class="mx-auto">
            <v-list>

                <v-list-item>
                    <v-list-item-title>
                        <strong>
                            <v-text-field
                            v-model="eventTitle"
                            label="Название мероприятия"
                            color="#5A009D"
                            ></v-text-field>

                            <v-text-field
                            v-model="eventPlace"
                            label="Место проведения"
                            color="#5A009D"
                            ></v-text-field>

                            <v-text-field
                            v-model="eventTime"
                            label="Время проведения"
                            color="#5A009D"
                            ></v-text-field>


                        </strong>
                    </v-list-item-title>

                    <v-btn @click="addPost" class="ma-1" outlined color="#5A009D" v-if="eventTitle && eventBody && eventPlace && eventTime">
                        Опубликовать
                    </v-btn>
                </v-list-item>

                <v-list-item>
                    <v-textarea
                        v-model="eventBody"
                        label="Описание мероприятия"
                        outlined
                        color="#5A009D"
                    ></v-textarea>
                </v-list-item>
                
            </v-list>
            </v-card>
            </v-col>
        </div>


        <v-col cols="10">
        <Post v-for="(event, index) in events.reverse()" 
        :key="index"
        
        :event_name="event.event_name"
        :event_place="event.event_place"
        :event_time="event.event_time"
        :event_description="event.event_description"
        :event_author_id="event.event_author_id"
        :event_author_login="profile.login"
        :event_reg_logins="event.event_reg_logins"
        :event_comments="event.event_comments"
        :event_id="event.event_id"
        :myId="myId"
        :user="user"
        
        ></Post>
        </v-col>
    </div>
</template>

<script>

import Post from '@/components/Post.vue'

export default {
    components: {
        Post
    },
    data(){
        return{
            profile: {},
            events: [],
            eventTitle: '',
            eventBody: '',
            eventPlace: '',
            eventTime: '',
        }
    },
    methods:{
        loadUser(){
            this.profile = {login:'',password:'',name:''}
            let url = 'http://188.225.47.187/api/jsonstorage/?id=b5fdb358d399fc57f59833491e41c652'
            this.$axios.get(url)
            .then(response=>{
                let users = response.data
                this.profile = users[this.$route.params.id]
            })
        },
        loadPosts(){
            let url = 'http://188.225.47.187/api/jsonstorage/?id=19ba6b6b92642c96559aaf1a3f853f66'
            this.$axios.get(url).then(response=>{
                let allEvents = response.data
                this.events = [];
                for(let event in allEvents){
                    if (allEvents[event].event_author_id == this.$route.params.id){
                        this.events.push(allEvents[event])
                    }
                }
            })
        },
        addPost(){
            this.$axios.get('http://188.225.47.187/api/jsonstorage/?id=19ba6b6b92642c96559aaf1a3f853f66')
                .then((response) => {
                    let allEvents = response.data
                    allEvents.push({
                        event_name: this.eventTitle,
                        event_id: allEvents.length,
                        event_place: this.eventPlace,
                        event_time: this.eventTime,
                        event_description: this.eventBody,
                        event_author_id: this.$route.params.id,
                        event_author_login: this.profile.login,
                        event_reg_logins: [this.profile.login],
                        event_comments: []
                    })

                    this.axios.put('http://188.225.47.187/api/jsonstorage/?id=19ba6b6b92642c96559aaf1a3f853f66', allEvents)
                        .then(() => {
                            this.loadPosts();
                            this.eventTitle = '';
                            this.eventBody = '';
                            this.eventPlace = '';
                            this.eventTime = '';
                            //this.loadPosts();
                        })
                })
        }
        
    },
    mounted(){
        this.loadUser();
        this.loadPosts();
        setInterval((() => this.loadPosts()), 500);
    },
    watch:{
        $route(){
            this.loadUser()
            this.loadPosts()
        }
    },
    props:['myId','user'],
}
</script>