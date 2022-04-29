<template>

        <select  name="{{title}}" v-model="select_model" id="">
            {{options}}
            <option  v-for="option in options" :key="option" :value="option">{{option}}</option>
        </select>
</template>

<script>



    export default {
        name: 'selectComponent',
        props:
            [
                'options'
            ],


    }
</script>



