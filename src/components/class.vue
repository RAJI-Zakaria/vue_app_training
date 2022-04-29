<template>
       <table class="class_table" border="1">
           <tr>
           <th>name</th>
           <th>level</th>
           </tr>
           <tr v-for="cls in class_s" :key="cls" style="">
              <td> {{cls.class_name}}</td>
               <td>{{cls.level}}</td>

           </tr>
       </table>


</template>

<script>
    export default {
        name: 'Class_s',
        props: [
            'class_s'
        ]
    }
</script>

<style scoped>
    .class_table{
        margin: 20px;
        /*margin-left: auto;*/
        /*margin-right: auto;*/
        border-collapse: collapse;
    }
    .class_table td, .class_table th{
        padding: 5px;
    }
</style>


