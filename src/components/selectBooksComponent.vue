<template>
    <label>{{title}}</label><br>
    <SelectComponent v-model="livre" :options="lst_options"/>
    <br>
    <button class="btn btn-success" v-on:click="addLivreFilter">add</button>
    <button v-on:click="deleteLivreFilter" class="btn btn-danger">delete</button><br>
   <SelectComponent :options="selected_options"
           v-model="filterLivre"
        multiple="true"/>
</template>

<script>


    import SelectComponent from "./selectComponent.vue";

    export default {
        name: 'selectBooksComponent',
        components:
            {
                SelectComponent
            },
        props:
            [
                'title',
                'lst_options',
            ],
        data() {
            return {
                selected_options:[],
                livre:'',
                filterLivre:''

            };
        },methods :{
            addLivreFilter(){
                var res = this.selected_options.indexOf(this.livre) === -1 ? this.selected_options.push(this.livre) : console.log("This item already exists");
                //send data to the parent
                this.$emit('selected-value', { selected_options: this.selected_options });

                return res;

            }
            ,
            deleteLivreFilter(){
                 var index = this.selected_options.indexOf(this.filterLivre[0]);
                var res = index >= 0 ? this.selected_options.splice(index, 1) : console.log("This item doesn't exist");

                this.$emit('selected-value', { selected_options: this.selected_options });

                return res;

            },


        }



    }
</script>



