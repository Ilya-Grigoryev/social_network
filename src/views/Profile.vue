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
                <img src="https://randomuser.me/api/portraits/men/7.jpg" style="max-width: 100%">
            </v-col>
            <v-col cols="10" class="text-left">
                <p>
                    Веб-сайт: <a href="..." target="_blank">{{profile.website}}</a>
                </p>
                <p>
                    E-mail: <a href="mailto:...">{{profile.email}}</a>
                </p>
                <p>
                    Город: {{profile.address.city}}
                </p>
                <p>
                    Место работы: ...
                </p>
            </v-col>
        </v-row>

        <v-card>
            <v-card-title></v-card-title>
        </v-card>

        ОСТАЛЬНОЕ СОДЕРЖИМОЕ СТРАНИЦЫ
    </div>
</template>

<script>
export default {
    data(){
        return{
            profile: null,
        }
    },
    methods:{
        loadUser(){
            let url = 'http://jsonplaceholder.typicode.com/users/' + this.$route.params.id
            this.$axios.get(url).then(response=>{
                this.profile = response.data
            })
        }
    },
    mounted(){
        this.loadUser()
    },
    watch:{
        $route(){
            this.loadUser()
        }
    }
}
</script>