<template>
    <div class="container">
        <h1>Comentários</h1>
        <hr />
        <div class="form-todo form-group">
            <p>
                <input type="text" placeholder="nome" name="author" class="form-control" v-model="name" />
            </p>
            <p>
                <textarea name="message" placeholder="Comentário" class="form-control" v-model="message" ></textarea>
            </p>
            <button type="submit" class="btn btn-primary" v-on:click="handleComment()">Comentar</button>
        </div>
        <div class="list-group" style="margin-top:1em" v-for="(comment, index) in allComments" :key="index">
            <div class="list-group-item">
                <span class="comment-author">
                    Autor:
                    <strong>{{ comment.name }}</strong>
                </span>
                <p>{{ comment.message }}</p>
                <div>
                    <a href="#" title="Excluir" v-on:click.prevent="handleRemove(index)">Excluir</a>
                </div>
            </div>
        </div>
        <hr />
    </div>
</template>

<script>
export default {
    data() {
        return {
            comments: [],
            name: '',
            message: ''
        }
    },
    methods: {
        handleComment() {
            // valida campo
            if (this.message.trim() === '') {
                return;
            }

            // popula objeto comments
            this.comments.push({
                name: this.name,
                message: this.message
            })

            // limpa campos
            this.name = '';
            this.message = '';
        },
        // Remove comentário
        handleRemove(index) {
            this.comments.splice(index, 1);
        }
    },
    computed: {
        allComments() {
            return this.comments.map((comment) => ({
                ...comment,
                name: comment.name === '' ? 'Anônimo' : comment.name
            }))
        }
    },
    watch: {
        message(val) {
            console.log("val", val);
        }
    }
}
</script>