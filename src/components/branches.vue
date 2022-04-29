<template>
    <ul>
        <li  v-for="branche in branches" v-bind:key="branche">
            {{ branche }}
        </li>
    </ul>
</template>

<script>
    export default {
        name: 'BranchesList',
        props:[
            'branches'
        ]

    }
</script>


