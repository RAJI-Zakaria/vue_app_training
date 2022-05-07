<template>

    <label>{{title}}</label><br>
    <input class="form-control" type="text" v-model="searchingStr" @change="search" placeholder="Search" />
    <input class="form-check-label" type="checkbox" value="false" @click="checkOption" v-model="check_enable">

</template>

<script>

    export default {
        name: 'searchComponentCheck',
        components:
            {

            },
        props:
            [
                'lst_options',
                'title'
            ],
        data() {
            return {
                check_enable: false,
                searchingStr:''
            };
        },methods :{
            getCheck(){
                return this.check_enable;

            },
            checkOption(){
                //changing the state of the check box from the true to false and vice versa.
                this.check_enable = !this.check_enable;
                this.$emit('check-box-state', { isChecked: this.check_enable })

            },
            search(){
                this.$emit('searchQuery', { query: this.searchingStr })

            }

        }



    }
</script>



