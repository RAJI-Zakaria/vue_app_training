<template>
   <div>
       <input class="form-control" type="text" v-model="searchQuery" placeholder="Search" /><br>
        <b>Ecole : </b><br>
       <SelectComponent v-model="ecole" :options="filteredEcoles"/><br>
       <b>Branche : </b><br>
       <SelectComponent v-model="branche" :options="filteredBranches"/><br>
       <b>classDomain : </b><br>
       <SelectComponent v-model="classDomain" :options="filteredClassDomain"/><br>
       <b>level : </b><br>
       <SelectComponent v-model="level" :options="filteredLevel"/><br>
       <div v-if="filteredBooks.length"><b>Sorted Length = {{ filteredBooks.length }}</b></div><br>
           <div v-for="book in filteredBooks" :key="book" style="">
               <BookElement :book="book"/>
           </div>
   </div>
</template>

<script>

    import _data from "../assets/data.json";
    import BookElement from "./BookElement.vue";
    import SelectComponent from "./selectComponent.vue";

    // SelectComponent


    export default {
        name: 'DisplayBooks',
        components:
            {
                BookElement,
                SelectComponent
            },
        data() {
            return {
                books: _data,
                searchQuery:'',
                ecole:'',
                branche:'',
                classDomain:'',
                level:'',
            };
        },
        computed: {
            filteredBooks (){
                var result =  this.books;
                //console.log(SelectComponent.props.options);

                //checking if the search bar contains something
                if(this.searchQuery){
                    result= this.books.filter((item)=>{
                        return item.name.toLowerCase().includes(this.searchQuery.toLowerCase());
                    })
                }
                //checking if the school has been selected
                if(this.ecole){
                    result= result.filter((item)=>{
                        console.log("================> "+item.school);
                        return item.school.toLowerCase().includes(this.ecole.toLowerCase());
                    })
                }

                //checking if the branche has been selected
                if(this.branche){
                    result= result.filter((item)=>{
                        console.log("================> "+item.branches);
                        for(var i=0; i< item.branches.length; i++){
                            if(item.branches[i].toLowerCase()==this.branche.toLowerCase()){
                                return item.branches;
                            }
                        }
                    });
                }


                //checking if the classDomain has been selected
                if(this.classDomain){
                    result= result.filter((item)=>{
                        for(var i=0; i< item.class.length; i++){

                            //checking if the level of class has been selected
                            if(this.level){
                            if(item.class[i].class_name.toLowerCase()==this.classDomain.toLowerCase() && item.class[i].level==this.level){
                                return item.class;
                            }
                            }else{
                                if(item.class[i].class_name.toLowerCase()==this.classDomain.toLowerCase()){
                                    return item.class;
                                }
                            }
                        }
                    });
                }else if(this.level){
                    result= result.filter((item)=>{
                        for(var i=0; i< item.class.length; i++){

                            //checking if the level of class has been selected
                            if(this.level){
                                if(item.class[i].level==this.level){
                                    return item.class;
                                }
                            }
                        }
                    });
                }



                return result;
            },
            filteredEcoles(){
                return this.books.map(item => item.school).filter((value, index, self) => self.indexOf(value) === index);
            },
            filteredBranches(){
               return this.books.map(item => item.branches[0]).filter((value, index, self) => self.indexOf(value) === index);
            },filteredClassDomain(){
                return this.books.map(item => item.class[0].class_name).filter((value, index, self) => self.indexOf(value) === index);

            },filteredLevel(){
                return this.books.map(item => item.class[0].level).filter((value, index, self) => self.indexOf(value) === index);

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


