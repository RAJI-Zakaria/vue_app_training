<template>
        <div  v-for="branche in branches" v-bind:key="branche">
            {{ branche }}
        </div>
</template>

<script>
    export default {
        name: 'BranchesList',
        props:[
            'branches'
        ]

    }
</script>


