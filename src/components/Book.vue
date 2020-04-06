<template>
    <ion-card v-if="skeleton" style="display: flex; max-height: 150px">
        <ion-thumbnail slot="start" style="width: 30%">
            <ion-skeleton-text animated></ion-skeleton-text>
        </ion-thumbnail>
        <div class="containerInfo" style="width: 70%; padding: 10px">
            <h5 style="font-weight: bold"><ion-skeleton-text animated></ion-skeleton-text></h5>
            <h5><ion-skeleton-text animated></ion-skeleton-text></h5>
        </div>
    </ion-card>

    <ion-card v-else-if="!skeleton" style="display: flex; max-height: 150px">
        <div style="width: 30%">
            <img v-if="book.volumeInfo.imageLinks" style="object-fit: cover" :src="book.volumeInfo.imageLinks.thumbnail" alt="">
        </div>
        <div class="containerInfo" style="width: 70%; padding: 10px">
            <h5 style="font-weight: bold">{{book.volumeInfo.title}}</h5>
            <h5 v-for="auth in book.volumeInfo.authors">{{auth}}</h5>
            <b>
                <router-link :to="{name: 'book', params: {id: book.id}}" style="text-decoration: none">Voir plus</router-link>
            </b>
        </div>
    </ion-card>
</template>

<script>
    export default {
        props: ['book', 'skeleton']
    }
</script>
<style lang="scss" scoped>
    .containerInfo {
        width: 70%;
        padding: 10px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;

        & * {
            margin: 0;
        }
    }
</style>
