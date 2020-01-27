<template>
    <div class="d-flex justify-center">
        <v-card width="600px" class="mt-12 pa-10">
            <v-card-title>
                Зарегистрируйтесь
            </v-card-title>

            <v-text-field
                label="Введите имя"
                v-model="name"
                outlined
            ></v-text-field>

            <v-text-field
                label="Введите логин"
                v-model="login"
                outlined
            ></v-text-field>

            <v-text-field
                label="Введите пароль"
                v-model="password"
                outlined
            ></v-text-field>

            <v-text-field
                label="Введите почту"
                v-model="email"
                outlined
            ></v-text-field>

            <v-text-field
                label="Введите город"
                v-model="city"
                outlined
            ></v-text-field>

            <v-text-field
                label="Введите компанию"
                v-model="company"
                outlined
            ></v-text-field>

            <v-text-field
                label="Введите веб-сайт"
                v-model="website"
                outlined
            ></v-text-field>

            <v-text-field
                label="Введите ссылку на фото"
                v-model="photo"
                outlined
            ></v-text-field>

            <v-btn @click="registration">
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
            website: '',
            email: '',
            city: '',
            company: '',
            photo: '',
        }
    },
    methods:{
        registration(){
            this.$axios.get('http://188.225.47.187/api/jsonstorage/8b1a4c15dc3951b4d9cde6c56e527448')
                .then((response) => {
                        let users = response.data
                        users.push({
                            login: this.login,
                            password: this.password,
                            name: this.name,
                            website: this.website,
                            email: this.email,
                            city: this.city,
                            company: this.company,
                            photo: this.photo
                        })

                        this.axios.put('http://188.225.47.187/api/jsonstorage/8b1a4c15dc3951b4d9cde6c56e527448', users);
                        this.$router.push('/login');
                })
        }
    },
}
</script>