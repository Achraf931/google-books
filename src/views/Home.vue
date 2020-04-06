<template>
    <div class="ion-page">
        <ion-header>
            <ion-toolbar>
                <ion-buttons slot="start">
                    <ion-back-button></ion-back-button>
                </ion-buttons>
                <ion-title>BOOKZ</ion-title>
            </ion-toolbar>
        </ion-header>
        <ion-item>
            <ion-label position="floating">Search</ion-label>
            <ion-input @keyup.enter="searchBook" @input="search = $event.target.value" :value="search"></ion-input>
        </ion-item>
        <ion-content>
            <Book v-for="(book, index) in books" :key="book.id" :book="book" :skeleton="skeleton"/>
        </ion-content>
    </div>
</template>

<script>
    import Book from '@/components/Book.vue'

    export default {
        name: 'Home',
        data() {
            return {
                search: '',
                books: [],
                skeleton: false
            }
        },
        components: {
            Book
        },
        methods: {
            searchBook() {
                this.skeleton = true
                if (this.search !== '')
                    this.$http.get(`https://www.googleapis.com/books/v1/volumes?q=${this.search}&orderBy=newest&maxResults=40&printType=books`).then(response => {
                        this.books = response.data.items
                            .filter((book, i, books) => books.findIndex((y) => y.id === book.id) === i)
                        this.skeleton = false
                    })
            }
        }
    }
</script>
