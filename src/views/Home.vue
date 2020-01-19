<template>
  <div class="home">
<!--    <img alt="Vue logo" src="../assets/logo.png"> -->
 <!--   <HelloWorld msg="Welcome to Your Vue.js App"/> -->

        <v-container fluid>

          <h1 class="green--text text--darken-2 text-left">
                  SocialLink
          </h1>
          <br>
          <h2 class="green--text text--darken-2 text-left">
                  Новый формат делового общения
          </h2>

          <v-row class="text-left">
            <v-col cols="6">
              <img src="./../assets/communication.jpg" width="410">
            </v-col>

            <v-col cols="6">
                <b>
                    text text text text text text text<br>
                    text text text text text text text<br>
                    text text text text text text text<br>
                    text text text text text text text<br>
                    text text text text text text text<br>
                    text text text text text text text<br>
                    text text text text text text text<br>
                    text text text text text text text<br>
                    text text text text text text text<br>
                    text text text text text text text<br>
                    text text text text text text text<br>
                </b>
            </v-col>
          </v-row>
        </v-container>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
//    HelloWorld
  }
}
</script>
