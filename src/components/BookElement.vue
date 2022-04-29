<template>
        <div>

                <div  v-on:click="showDetails()" class="header" >
                    <b>{{book.name}}</b>
                </div>
                <BookDetails  v-show="isInfosVisible" v-bind:single_book="book" />

        </div>
</template>

<script>

    import BookDetails from "./bookDetails.vue";



    export default {
        name: 'BookElement',
        components:
            {
                BookDetails
            },
        props:
            [
                'book'
            ],
        data() {
            return {
                isInfosVisible: false,
            };
        },
        methods: {
            showDetails(){
                this.isInfosVisible = !this.isInfosVisible;
                console.log(this);
            }
        }
    }
</script>

<style scoped>
    li:nth-child(even) {
        background-color: #f2f2f2;
    }

    .header{
        background: #2c3e50;
        color: #fff;
        padding: 20px;
            border-bottom: 1px solid black;
    }
</style>


