<template>
    <div class="d-flex justify-center">
        <v-card width="600px" class="mt-12 pa-10">
            <v-card-title>
                Войдите в аккаунт
            </v-card-title>

            <v-text-field
                label="Введите логин"
                v-model="login"
                outlined
                color="green"
            ></v-text-field>

            <v-text-field
                label="Введите пароль"
                v-model="password"
                outlined
                color="green"
            ></v-text-field>

            <v-btn @click="authenticate" color="green" outlined>
                Войти
            </v-btn>
            <br><br><br>
            
            Нет аккаунта? <router-link color="green" to="/registr">Регистрация</router-link>
        </v-card>
    </div>
</template>

<script>
export default {
    data(){
        return{
        }
    },
    methods:{
        authenticate(){
            this.axios.get('http://188.225.47.187/api/jsonstorage/?id=b5fdb358d399fc57f59833491e41c652')
                .then(
                    (response) => {
                        let users = response.data;
                        let found = false;
                        for(let index in users){
                            if(this.login == users[index].login && this.password == users[index].password){
                                this.$emit('login', index);
                                this.$router.push('/profile/' + index);
                                found = true;
                                break;
                            }
                        }
                        if(!found)
                            window.alert('Неверный логин или пароль!')
                    }
                )
        }
    },
}
</script>