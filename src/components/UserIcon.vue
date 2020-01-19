<template>
  <div class="home">
<!--    <img alt="Vue logo" src="../assets/logo.png"> -->
 <!--   <HelloWorld msg="Welcome to Your Vue.js App"/> -->

        <v-card
    max-width="650"
    style="padding: 17px;"
  >
    <v-row>
    <v-col cols="4" class="text-right">
        <v-list-item>
        <v-list-item-avatar center width="100" height="100">
            <img :src="getSrc">
            </v-list-item-avatar>
        </v-list-item>
    </v-col>
      <v-divider vertical class="my-0"></v-divider>
    
    <v-col cols="6" class="text-left">
    <v-list-item>
        
            <v-list-item-content>
                <h5 class="headline">{{name}}</h5>
                <v-list-item-subtitle>{{username}}</v-list-item-subtitle>
            </v-list-item-content>
       
    </v-list-item>

        <v-card-actions>
            <v-btn class="ma-2" outlined color="success"  link :to="getLink">
                <v-icon left>mdi-account-card-details-outline</v-icon>
                ПЕРЕЙТИ В ПРОФИЛЬ
            </v-btn>
        </v-card-actions>
    </v-col>

    </v-row>    
  </v-card>
  </div>
</template>

<script>
export default {
  props: ['name', 'username', 'id'],
  data: () => ({
  }),
  computed:{
      getSrc:function(){
          return 'https://randomuser.me/api/portraits/men/'+ this.id +'.jpg'
      },
      getLink:function(){
          return '/profile/' + this.id
      }
  }
}
</script>