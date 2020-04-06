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
            <div id="viewerCanvas" style="width: 100%; height: 100%"></div>
        </ion-content>
    </div>
</template>
<script>
    export default {
        name: 'viewer',
        mounted() {
            setTimeout(() => {
                this.initialize()
            }, 2000)
        },
        methods: {
            initialize() {
                console.log(this.$route.params.id)
                let viewer = new google.books.DefaultViewer(document.getElementById('viewerCanvas'))
                viewer.load(this.$route.params.id)
            }
        }
    }
</script>
