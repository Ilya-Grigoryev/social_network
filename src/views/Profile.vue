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
                <img :src="avatar" style="max-width: 100%">
            </v-col>
            <v-col cols="10" class="text-left">
                <p>
                    Веб-сайт: <a :href="profile.website" target="_blank">{{profile.website}}</a>
                </p>
                <p>
                    E-mail: <a href="mailto:...">{{profile.email}}</a>
                </p>
                <p>
                    Город: {{profile.address.city}}
                </p>
                <p>
                    Место работы: {{profile.company.name}}
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
            profile: null,
            posts: null,
            avatar: '',
        }
    },
    methods:{
        loadUser(){
            let url = 'http://jsonplaceholder.typicode.com/users/' + this.$route.params.id
            this.$axios.get(url).then(response=>{
                this.profile = response.data
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
        this.avatar = 'https://randomuser.me/api/portraits/men/'+ this.$route.params.id +'.jpg'
    },
    watch:{
        $route(){
            this.loadUser()
            this.loadPosts()
            this.avatar = 'https://randomuser.me/api/portraits/men/'+ this.$route.params.id +'.jpg'
        }
    }
}
</script>