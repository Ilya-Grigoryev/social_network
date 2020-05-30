<template>
  <div class="home">
      <v-row>
          <v-col cols="10">
            <Post v-for="(event, index) in events.reverse()" 
                :key="index"
                
                :event_name="event.event_name"
                :event_place="event.event_place"
                :event_time="event.event_time"
                :event_description="event.event_description"
                :event_author_id="event.event_author_id"
                :event_author_login="event.event_author_login"
                :event_reg_logins="event.event_reg_logins"
                :event_comments="event.event_comments"
                :event_id="event.event_id"
                :myId="myId"
                :user="user"
            
            ></Post>
          </v-col>
      </v-row>
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
      events: [],
    }
  },
  methods:{
    loadPosts(){
            let url = 'http://188.225.47.187/api/jsonstorage/?id=19ba6b6b92642c96559aaf1a3f853f66'
            this.$axios.get(url).then(response=>{
                let allEvents = response.data
                this.events = []
                for(let event in allEvents){
                    this.events.push(allEvents[event])
                }
            })
        },
  },
  mounted(){
        this.loadPosts();
        setInterval(() => this.loadPosts(), 500);
  },
  watch:{
    $route(){
        this.loadPosts()
    }
  },
    props:['myId','user'],
}
</script>