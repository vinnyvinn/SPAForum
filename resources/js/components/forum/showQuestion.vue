<template>
<v-card>
    <v-container fluid>
    <v-card-title>
    <div>
        <div class="headline">
            {{question.title}}
        </div>
        <span class="grey--text">{{question.user}} said {{question.created    }}</span>
    </div>

        <v-spacer></v-spacer>
    <v-btn color="teal" dark>{{question.reply_count}} Replies</v-btn>
    </v-card-title>
        <v-card-text v-html="body"></v-card-text>
        <v-card-actions v-if="own">
            <v-btn icon small @click="edit">
                <v-icon  color="orange">edit</v-icon>
            </v-btn>
            <v-btn icon small @click="destroy">
                <v-icon  color="red">delete</v-icon>
            </v-btn>

        </v-card-actions>
    </v-container>
</v-card>
</template>

<script>



    export default {
        props:['question'],
        data(){
          return {
              own:User.own(this.question.user_id)
          }
        },
        computed:{
            body(){
                return md.parse(this.question.body);
            }
        },
        methods:{
            destroy(){
                axios.delete(`/api/question/${this.question.id}`)
                    .then(res => this.$router.push('/forum'))
                    .catch(error => console.log(error.response.data))
            },
            edit(){
                eventBus.$emit('startEditing');
            }
        },

    }
</script>

<style scoped>

</style>
