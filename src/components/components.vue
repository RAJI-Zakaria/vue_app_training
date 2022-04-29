<template>
        <span v-for="(cmp, index) in component_s" :key="cmp" style="">
            {{cmp}}<span v-if="index+1 < component_s.length">, </span>
        </span>
</template>

<script>
    export default {
        name: 'Component_s',
        props: [
            'component_s'
        ]
    }
</script>


