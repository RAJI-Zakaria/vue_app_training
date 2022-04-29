<template>
       <table border="1">
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


