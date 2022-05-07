<template>

    <span>{{title}}</span> -
   <span v-if="lst_options.length"><b>Nbr items = {{ lst_options.length }}</b></span><br>
     <SelectComponent v-model="selected_option"  @change="getSelectedOption" :options="lst_options" />
    <input type="checkbox" value="false" @click="checkOption" v-model="check_enable">
</template>

<script>


    import SelectComponent from "./selectComponent.vue";

    export default {
        name: 'selectComponentCheck',
        components:
            {
                SelectComponent
            },
        props:
            [
                'title',
                'lst_options'
            ],
        data() {
            return {
                check_enable: false,
                selected_option:''
            };
        },methods :{
            getCheck(){
                return  this.check_enable;

            },
            checkOption(){
                //changing the state of the check box from the true to false and vice versa.
                this.check_enable = !this.check_enable;
                this.$emit('check-box-state', { isChecked: this.check_enable})

            },
            getSelectedOption(){
                this.$emit('selected-value', { selected_option: this.selected_option })

            }

        }



    }
</script>



