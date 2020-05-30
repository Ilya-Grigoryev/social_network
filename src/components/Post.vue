<template>
<div>
  <v-card
    max-width="1000"
    class="mx-auto"
  >
  <v-row>
  <v-col cols="4">
    <v-list-item>
      <v-list-item-content style="text-align: left;">
        <v-list-item-title>
          <strong>{{event_name}}</strong>
        </v-list-item-title>
        <v-list-item-subtitle>Организатор: <strong>{{event_author_login}}</strong></v-list-item-subtitle>
        <v-list-item-subtitle>Время: <strong>{{event_time}}</strong></v-list-item-subtitle>
        <v-list-item-subtitle>Место: <strong>{{event_place}}</strong></v-list-item-subtitle>
        <v-list-item-subtitle>Записались: <strong>{{event_reg_logins.join(', ')}}</strong></v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

    <v-card-text style="text-align: left;">
      {{event_description}}
    </v-card-text>
    </v-col>

    <v-col cols="8">
      <v-list-item>
      <v-list-item-content style="text-align: left;">
        <v-list-item-title>
          <strong>Комментарии:</strong>
        </v-list-item-title>
        <v-card-text style="text-align: left;">
            <v-list-item v-for="(comment, index) in event_comments" :key="index">
                <v-card class="mx-auto" width="600">
                    <v-list-item-title>
                       <router-link :to="'/profile/'+comment.comment_author_id">{{comment.comment_author_login}}</router-link>
                    </v-list-item-title>
                    <v-list-item>
                        {{comment.comment_text}}
                    </v-list-item>
                </v-card>
            </v-list-item>
            <v-list-item>
              <v-card width="600">
                    <v-text-field
                        v-model="commentText"
                        label="Комментировать"
                        color="#5A009D"
                    ></v-text-field>
                    <v-btn @click="addComment" class="ma-1" outlined color="#5A009D" v-if="commentText">Добавить</v-btn>
              </v-card>
             </v-list-item>
        </v-card-text>
        
      </v-list-item-content>
    </v-list-item>
    </v-col>
    </v-row>
    
    <v-btn @click="sign_up()" class="ma-1" outlined color="#5A009D">
          <div v-if="event_reg_logins.indexOf(user.login) == -1">
                  Записаться
          </div>
          <div v-else>
                  Отписаться
          </div>
      </v-btn>
  </v-card>
  <br><br>
</div>
</template>

<script>
export default {
  props: ['event_name', 
          'event_place', 
          'event_time', 
          'event_description', 
          'event_author_id', 
          'event_author_login', 
          'event_reg_logins', 
          'event_comments',
          'event_id',
          'myId', 'user'],
  data: () => ({
    commentText: '',
  }),
  methods:{
      addComment(){
            let url = 'http://188.225.47.187/api/jsonstorage/?id=19ba6b6b92642c96559aaf1a3f853f66'
            this.$axios.get(url).then(response=>{
                var allEvents = response.data
                allEvents[parseInt(this.event_id)]['event_comments'].push(
                  {
                        comment_author_id: this.myId,
                        comment_author_login: this.user.login,
                        comment_text: this.commentText
                  })
                this.axios.put('http://188.225.47.187/api/jsonstorage/?id=19ba6b6b92642c96559aaf1a3f853f66', allEvents)
                this.commentText = '';
            })
        },
        sign_up(){
            let url = 'http://188.225.47.187/api/jsonstorage/?id=19ba6b6b92642c96559aaf1a3f853f66'
            this.$axios.get(url).then(response=>{
                var allEvents = response.data
                if (this.event_reg_logins.indexOf(this.user.login) != -1){
                    allEvents[parseInt(this.event_id)]['event_reg_logins'].splice(allEvents[parseInt(this.event_id)]['event_reg_logins'].indexOf(this.user.login), 1);
                    this.event_reg_logins.splice(this.event_reg_logins.indexOf(this.user.login), 1);
                }else{
                    allEvents[parseInt(this.event_id)]['event_reg_logins'].push(this.user.login);
                    this.event_reg_logins.push(this.user.login);
                }
                console.log(this.event_reg_logins);
                this.axios.put('http://188.225.47.187/api/jsonstorage/?id=19ba6b6b92642c96559aaf1a3f853f66', allEvents)

            })
        }
  },
}
</script>
