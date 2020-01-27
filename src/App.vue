<template>
   <v-app id="app">
      <v-navigation-drawer  color="green"
                            dark
                            expand-on-hover
                            hide-overlay
                            permanent
                            right
                            app>

      <v-list nav shaped dense>
        <v-list-item two-line>
          <v-list-item-avatar>
            <img :src="user.photo">
          </v-list-item-avatar>
          <v-list-item-content class="text-left">
            <v-list-item-title class="font-weight-black">SocialLink</v-list-item-title>
            <v-list-item-subtitle>{{user.name}}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        <v-divider class="my-3"></v-divider>


        <v-list-item link to="/">
          <v-list-item-icon>
            <v-icon>mdi-home-outline</v-icon>
          </v-list-item-icon>
          <v-list-item-content class="text-left">
            <v-list-item-title class="text-left">Главная</v-list-item-title>
          </v-list-item-content>
        </v-list-item>


        <v-list-item link :to="'/profile/'+id">
          <v-list-item-icon>
            <v-icon>mdi-account-outline</v-icon>
          </v-list-item-icon>
          <v-list-item-content class="text-left">
            <v-list-item-title class="text-left">Мой профиль</v-list-item-title>
          </v-list-item-content>
        </v-list-item>


        <v-list-item link to="/users">
          <v-list-item-icon>
            <v-icon>mdi-account-multiple-plus-outline</v-icon>
          </v-list-item-icon>
          <v-list-item-content class="text-left">
            <v-list-item-title class="text-left">Найти друзей</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        

      </v-list>

      </v-navigation-drawer>
    
    <v-content class="px-12 py-3">
      <v-container fluid>
        <router-view v-on:login="updateUser" :user="user" :myId="id"/>
      </v-container>
    </v-content>

  </v-app>
</template>


<script>
export default {
  data(){
    return{
        user: {},
        id: null,
    }
  },
  methods:{
      updateUser(index){
        this.axios.get('http://188.225.47.187/api/jsonstorage/8b1a4c15dc3951b4d9cde6c56e527448')
                .then(
                    (response) => {
                        let users = response.data;
                        this.user = users[index];
                        this.id = index;
                    }
                )
      },
  },
  mounted(){
        if (this.id == null)
            this.$router.push('/login');
    },
}
</script>



<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
