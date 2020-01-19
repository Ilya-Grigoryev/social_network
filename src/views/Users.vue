<template>
  <div class="home">
<!--    <img alt="Vue logo" src="../assets/logo.png"> -->
 <!--   <HelloWorld msg="Welcome to Your Vue.js App"/> -->

  <v-row>
    <v-col cols="6">
    <UserIcon 
        :name="users[0].name"
        :username="users[0].username"
        id=1
    ></UserIcon>
    </v-col>
    <v-col cols="6">
    <UserIcon 
        :name="users[1].name"
        :username="users[1].username"
        id='2'
    ></UserIcon>
    </v-col>
  </v-row>

  <v-row>
    <v-col cols="6">
    <UserIcon 
        :name="users[2].name"
        :username="users[2].username"
        id=3
    ></UserIcon>
    </v-col>
    <v-col cols="6">
    <UserIcon 
        :name="users[3].name"
        :username="users[3].username"
        id='4'
    ></UserIcon>
    </v-col>
  </v-row>

  <v-row>
    <v-col cols="6">
    <UserIcon 
        :name="users[4].name"
        :username="users[4].username"
        id=5
    ></UserIcon>
    </v-col>
    <v-col cols="6">
    <UserIcon 
        :name="users[5].name"
        :username="users[5].username"
        id='6'
    ></UserIcon>
    </v-col>
  </v-row>

  <v-row>
    <v-col cols="6">
    <UserIcon 
        :name="users[6].name"
        :username="users[6].username"
        id='7'
    ></UserIcon>
    </v-col>
    <v-col cols="6">
    <UserIcon 
        :name="users[7].name"
        :username="users[7].username"
        id='8'
    ></UserIcon>
    </v-col>
  </v-row>

  <v-row>
    <v-col cols="6">
    <UserIcon 
        :name="users[8].name"
        :username="users[8].username"
        id='9'
    ></UserIcon>
    </v-col>
    <v-col cols="6">
    <UserIcon 
        :name="users[9].name"
        :username="users[9].username"
        id='10'
    ></UserIcon>
    </v-col>
  </v-row>
  
  </div>
</template>

<script>
import UserIcon from '@/components/UserIcon.vue'

export default {
  components: {
    UserIcon
  },
  data(){
    return{
      users: [],
    }
  },
  methods:{
    loadUsers(){
      let url = 'http://jsonplaceholder.typicode.com/users'
        this.$axios.get(url).then(response=>{
          this.users = response.data
      })
    }
  },
  mounted(){
        this.loadUsers()
  },
  watch:{
    $route(){
        this.loadUsers()
    }
  }
}
</script>