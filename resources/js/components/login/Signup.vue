<template>
<div>
    <v-form @submit.prevent="signup">
        <v-container grid-list-xl>
            <v-layout wrap>
                <v-flex
                    xs12
                    md4
                >
                    <v-text-field
                        v-model="form.name"
                        label="Name"
                        type="text"
                        required
                    ></v-text-field>
                    <span class="red--text" v-if="errors.name">{{errors.name[0]}}</span>
                </v-flex>
                <v-flex
                    xs12
                    md4
                >
                    <v-text-field
                        v-model="form.email"
                        label="E-mail"
                        type="email"
                        required
                    ></v-text-field>
                    <span class="red--text" v-if="errors.email">{{errors.email[0]}}</span>
                </v-flex>

                <v-flex
                    xs12
                    md4
                >
                    <v-text-field
                        v-model="form.password"
                        label="Password"
                        type="password"
                        required
                    ></v-text-field>

                    <v-text-field
                        v-model="form.password_confirmation"
                        label="Password"
                        type="password"
                        required
                    ></v-text-field>
                    <span class="red--text" v-if="errors.password">{{errors.password[0]}}</span>
                </v-flex>
                <v-flex
                    xs12
                    md4
                >
                    <v-btn
                        color="green"
                        type="submit"
                    >Sign Up</v-btn>
                    <router-link to="/login">
                        <v-btn color="blue">Login</v-btn>
                    </router-link>
                </v-flex>
            </v-layout>
        </v-container>
    </v-form>
</div>
</template>

<script>
    export default {
       data(){
           return{
               form:{
                   name:null,
                   email:null,
                   password:null,
                   password_confirmation:null
               },
               errors:{}
           }
       },
        created(){
            if(User.loggedIn()){
                this.$router.push({name:'forum'});
            }
        },
        methods:{
           signup(){
            axios.post('api/auth/signup',this.form)
                .then(res => {
                    User.responseAfterLogin(res);

                })
               .catch(error => this.errors = error.response.data)
           }
        }
    }
</script>

<style scoped>

</style>
