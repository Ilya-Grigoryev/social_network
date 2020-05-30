<template>
  <div class="home">
<UserIcon v-for="(user, id) in users" :key="id"
    :name="user.name"
    :username="user.login"
    :id="id"

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
      let url = 'http://188.225.47.187/api/jsonstorage/?id=b5fdb358d399fc57f59833491e41c652'
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