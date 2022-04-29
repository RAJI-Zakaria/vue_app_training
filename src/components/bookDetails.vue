<template>
                <div>
                    <b>book</b> : {{single_book.book}}<br>
                    <b>school</b> : {{single_book.school}}<br>
                    <b>branches</b> :  <Branches v-bind:branches="single_book.branches"/> <br>
                    <b>class</b> :  <Class_s v-bind:class_s="single_book.class"/>
                    <b>components</b> : <Component_s v-bind:component_s="single_book.components"/><br>
                    <b>castingTime</b> : <p v-html="single_book.castingTime"></p><br>
                    <b>scope</b> : {{single_book.scope}}<br>
                    <b>Description</b> : <p v-html="single_book.description"></p>
                    <b>Nécessaire</b> : <p v-html="single_book.necessary"></p>
                </div>
</template>


<script>

    import Branches from "./branches.vue";
    import Class_s from "./class.vue";
    import Component_s from "./components.vue";



    // data.forEach(obj => {
    //     Object.entries(obj).forEach(([key, value]) => {
    //         console.log(`${key} ${value}`);
    //     });
    //     console.log('-------------------');
    // });

    // ....
    export default {
        name: 'bookDetails',
        components:
            {
                Branches,
                Class_s,
                Component_s
            },
         props:
             [
                 'single_book'
             ]
    }
</script>

<style scoped>
    li:nth-child(even) {
        background-color: #f2f2f2;
    }
</style>


