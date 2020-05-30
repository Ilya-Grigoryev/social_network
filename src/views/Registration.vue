<template>
    <div class="d-flex justify-center">
        <v-card width="600px" class="mt-12 pa-10">
            <v-card-title>
                Зарегистрируйтесь
            </v-card-title>

            <v-text-field
                color="#5A009D"
                label="Введите имя"
                v-model="name"
                outlined
            ></v-text-field>

            <v-text-field
                color="#5A009D"
                label="Введите логин"
                v-model="login"
                outlined
            ></v-text-field>

            <v-text-field
                color="#5A009D"
                label="Введите пароль"
                v-model="password"
                outlined
            ></v-text-field>

            <v-btn @click="registration" color="#5A009D" outlined>
                Зарегистрироваться
            </v-btn>
        </v-card>
    </div>
</template>

<script>
export default {
    data(){
        return{
            login: '',
            password: '',
            name: '',
        }
    },
    methods:{
        registration(){
            this.$axios.get('http://188.225.47.187/api/jsonstorage/?id=b5fdb358d399fc57f59833491e41c652')
                .then((response) => {
                    let users = response.data
                    users.push({
                        name: this.name,
                        login: this.login,
                        password: this.password,
                    })

                    this.axios.put('http://188.225.47.187/api/jsonstorage/?id=b5fdb358d399fc57f59833491e41c652', users);
                    this.$router.push('/login');
                })
        }
    },
}
</script>