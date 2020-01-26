<template>
  <div class="home">
<!--    <img alt="Vue logo" src="../assets/logo.png"> -->
 <!--   <HelloWorld msg="Welcome to Your Vue.js App"/> -->

<UserIcon v-for="(user, id) in users" :key="id"
    :name="user.name"
    :username="user.login"
    :id="id"
    :photo="user.photo"

></UserIcon>
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
      let url = 'http://188.225.47.187/api/jsonstorage/8b1a4c15dc3951b4d9cde6c56e527448'
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