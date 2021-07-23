<template>
    <div>
        <button class="btn btn-success float-right" @click="onNew">
            New Book
        </button>
        <h5>Book View</h5>
        <hr>

        <form action="" @submit.prevent="onSave">
            <b-form-group label="Author">
                <b-form-input v-model="book.author"></b-form-input>
            </b-form-group>

            <b-form-group label="Title">
                <b-form-input v-model="book.title"></b-form-input>
            </b-form-group>

            <b-form-group label="Genre">
                <b-form-input v-model="book.genre"></b-form-input>
            </b-form-group>

            <b-form-group label="Description">
                <b-form-input v-model="book.description"></b-form-input>
            </b-form-group>

            <b-form-group label="Status">
                <b-form-input v-model="book.status"></b-form-input>
            </b-form-group>
    
            <b-form-group>
                <button class="btn btn-primary" type="submit">Save Changes</button>
                <button class="btn btn-danger float-right" type="button" @click="onDelete" v-if="book.id">Delete Book</button>
            </b-form-group>
        </form>
    </div>
</template>

<script>
export default {
    props: {
        book: {},
        
    },
    methods: {
        async onSave() {
            try {
                if(!this.book.id) {
                    await this.$axios.post('/api/books', this.book)
                }else{
                    await this.$axios.put('/api/books/' + this.book.id, this.book)
                }

                this.$emit('saved')
            } catch (err) {
                alert(err.response.data.message)
            }
        },
        onNew() {
            this.$emit('newBook')
        },
        async onDelete() {
            try {
                this.$axios.delete('/api/books/' + this.book.id)
                this.$emit('deleted')
            } catch (err) {
                alert(err.response.data.message)
            }
        }
    }
}
</script>