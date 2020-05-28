<template>
  <div class="home">
<!--    <img alt="Vue logo" src="../assets/logo.png"> -->
 <!--   <HelloWorld msg="Welcome to Your Vue.js App"/> -->

        <v-card
    max-width="650"
    style="padding: 17px;"
  >
    <v-row>
      <v-divider vertical class="my-0"></v-divider>
    
    <v-col cols="6" class="text-left">
    <v-list-item>
        
            <v-list-item-content>
                <h5 class="headline">{{name}}</h5>
                <v-list-item-subtitle>{{username}}</v-list-item-subtitle>
            </v-list-item-content>
       
    </v-list-item>

        <v-card-actions>
                <v-btn class="ma-2" outlined color="#5A009D"  link :to="'/profile/'+id">ПЕРЕЙТИ В ПРОФИЛЬ</v-btn>
        </v-card-actions>
    </v-col>

    </v-row>   
  </v-card>
  <br>
  </div>
</template>

<script>
export default {
  props: ['name', 'username', 'id'],
  data: () => ({

  }),
}
</script>