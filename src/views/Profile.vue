<template>
    <div :v-if="profile!== null">
        <v-row class="text-left">
            <v-col cols="10">
                <h1 class="green--text text--darken-2">
                    <v-icon large color="green darken-2">mdi-account-outline</v-icon>
                    {{profile.name}}
                </h1>
            </v-col>
        </v-row>
        <v-row class="text-left">
            <v-col cols="2">
                <img :src="profile.photo" style="max-width: 100%">
            </v-col>
            <v-col cols="10" class="text-left">
                <p>
                    Веб-сайт:    {{profile.website}}
                </p>
                <p>
                    E-mail: <a href="mailto:...">{{profile.email}}</a>
                </p>
                <p>
                    Город: {{profile.city}}
                </p>
                <p>
                    Место работы: {{profile.company}}
                </p>
            </v-col>
        </v-row>

        <v-col cols="10">
        <Post v-for="(post, index) in posts" 
        :key="index"
        
        :title="post.title"
        :body="post.body"
        :author="profile.name"
        :avatar="avatar"
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
            posts: null,
        }
    },
    methods:{
        loadUser(){
            this.profile = {login:'',password:'',name:'',website:'',email:'',city:'',company:'',photo:''}
            let url = 'http://188.225.47.187/api/jsonstorage/8b1a4c15dc3951b4d9cde6c56e527448'
            this.$axios.get(url)
            .then(response=>{
                let users = response.data
                this.profile = users[this.$route.params.id]
            })
        },
        loadPosts(){
            let url = 'http://jsonplaceholder.typicode.com/posts?userId=' + this.$route.params.id
            this.$axios.get(url).then(response=>{
                this.posts = response.data
            })
        },
        
    },
    mounted(){
        this.loadUser()
        this.loadPosts()
    },
    watch:{
        $route(){
            this.loadUser()
            this.loadPosts()
        }
    },
    props:['myId'],
}
</script>