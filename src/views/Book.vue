<template>
    <div class="ion-page">
        <ion-header>
            <ion-toolbar>
                <ion-buttons style="margin-left: 15px; color: red" @click="$router.go(-1)" slot="start">Back
                </ion-buttons>
                <ion-title>BOOKZ</ion-title>
            </ion-toolbar>
        </ion-header>

        <ion-content>
            <ion-card>
                <ion-card-header>
                    <img :src="thumbnail" alt="">
                    <ion-card-title>{{book.title}}</ion-card-title>
                </ion-card-header>

                <ion-card-content v-html="book.description">
                    {{book.description}}
                </ion-card-content>
                <router-link :to="{name: 'viewer', params: {id: id}}" style="text-decoration: none">Voir plus</router-link>
            </ion-card>
        </ion-content>
    </div>
</template>

<script>
    export default {
        name: 'book',
        data() {
            return {
                book: {},
                thumbnail: '',
                id: ''
            }
        },
        mounted() {
            this.$http.get(`https://www.googleapis.com/books/v1/volumes/${this.$route.params.id}`).then(response => {
                this.book = response.data.volumeInfo
                this.id = response.data.id
                this.thumbnail = response.data.volumeInfo.imageLinks.thumbnail
            }).catch(err => {
                this.$router.replace('/')
            })
        }
    }
</script>
