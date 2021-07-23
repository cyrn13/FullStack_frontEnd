<template>
    <div>
        <NavBar />
        <div class="container">
            <h1>My Books</h1>
            <div class="row">
                <div class="col-6">
                    <h5>List of Books</h5>
                    <hr>
                    <ul class="list-group">
                        <li class="list-group-item btn-li"  v-for="book in books" :key="book.id" @click="onSelected(book)">
                            {{book.author}} <span class="float-right">{{book.title}}</span>
                        </li>
                    </ul>
                </div>
                <div class="col-4">
                    <BookView :book="selectedBook" @saved="onChange" @newBook="onNew" @deleted="onChange" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            books: [],
            selectedBook: {}
        }
    },
    methods: {
        async getMyBooks() {
            await this.$axios.get('/api/books')
            .then((res)=>{
                if(res.status==200) {
                    this.books = res.data
                }
            })
        },
        onChange() {
            this.getMyBooks()
            this.selectedBook = {}
        },
        onSelected(book) {
            this.selectedBook = book;
        },
        onNew() {
            this.selectedBook = {}
        },
    },
    created() {
        this.getMyBooks()
    }
}
</script>