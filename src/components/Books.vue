<template>
   <div>
       <input class="form-control" type="text" v-model="searchQuery" placeholder="Search" />

       <select  name="" id="">
           <option  v-for="ecole in filteredEcoles" :key="ecole" :value="ecole">{{ecole}}</option>
       </select>


       <ul>
           <li v-for="book in filteredBooks" :key="book" style="">
               <BookElement :book="book"/>
           </li>
       </ul>
   </div>
</template>

<script>

    import _data from "../assets/data.json";
    import BookElement from "./BookElement.vue";



    export default {
        name: 'DisplayBooks',
        components:
            {
                BookElement
            },
        data() {
            return {
                books: _data,
                searchQuery:'',
                ecoles:'',
            };
        },
        computed: {
            filteredBooks (){
                var result = [];
                if(this.searchQuery){
                    result= this.books.filter((item)=>{
                        return item.name.toLowerCase().includes(this.searchQuery.toLowerCase());
                    })
                }else{
                    result= this.books;
                }

                return result;
            },
            filteredEcoles(){
                return this.books.map(item => item.school).filter((value, index, self) => self.indexOf(value) === index);
            }
        }

    }
</script>

<style scoped>
    li:nth-child(even) {
        background-color: #f2f2f2;
    }

    .header{
        background: #2c3e50;
        color: #fff;
        padding: 20px;
    }
</style>


