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


        <div style="text-align: left;" v-if="this.$route.params.id == myId">
            <v-col cols="10">
            <v-card outlined max-width="1000" class="mx-auto">
            <v-list>

                <v-list-item>
                    <v-list-item-title>
                        <strong>
                            <v-text-field
                            v-model="postTitle"
                            label="Заголовок поста"
                            color="green"
                            ></v-text-field>
                        </strong>
                    </v-list-item-title>

                    <v-btn @click="addPost()" class="ma-3" outlined color="green">Опубликовать</v-btn>
                </v-list-item>

                <v-list-item>
                    <v-textarea
                        v-model="postBody"
                        label="Сам пост"
                        outlined
                        color="green"
                    ></v-textarea>
                </v-list-item>
                
            </v-list>
            </v-card>
            </v-col>
        </div>


        <v-col cols="10">
        <Post v-for="(post, index) in posts" 
        :key="index"
        
        :title="post.title"
        :body="post.body"
        :author="profile.name"
        :avatar="profile.photo"
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
            posts: [],
            postTitle: '',
            postBody: '',
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
            let url = 'http://188.225.47.187/api/jsonstorage/1ac7b4adad563ea2b602d7588601f9f8'
            this.$axios.get(url).then(response=>{
                let allPosts = response.data
                this.posts = []
                for(let post in allPosts){
                    if (allPosts[post].userId == this.$route.params.id){
                        this.posts.push(allPosts[post])
                    }
                }
            })
        },
        addPost(){
            this.$axios.get('http://188.225.47.187/api/jsonstorage/1ac7b4adad563ea2b602d7588601f9f8')
                .then((response) => {
                    let allPosts = response.data
                    allPosts.unshift({
                        userId: this.myId,
                        title: this.postTitle,
                        body: this.postBody
                    })

                    this.axios.put('http://188.225.47.187/api/jsonstorage/1ac7b4adad563ea2b602d7588601f9f8', allPosts)
                        .then(() => {
                            this.loadPosts();
                            this.postTitle = '';
                            this.postBody = '';
                        })
                })
        }
        
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