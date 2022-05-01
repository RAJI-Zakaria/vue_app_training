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
       <b>Livres : </b><br>
       <SelectComponent v-model="livre" :options="filteredLivres"/>
       <br><button class="btn" v-on:click="addLivreFilter">add</button><button v-on:click="deleteLivreFilter" class="btn">delete</button><br>
       <SelectComponent v-model="filterLivre" @change="filterLivreOnChange($event)" :options="filteredSearchedLivres" multiple="true"/>


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
                filteredSearchedLivres: [],
                filterLivre: ''

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

                if(this.filteredSearchedLivres.length>0){
                    result= result.filter((item)=>{
                        for(var i=0; i< this.filteredSearchedLivres.length; i++){
                            if(item.book == this.filteredSearchedLivres[i]){
                                return item;
                            }
                        }
                    });
                }




                return result;
            },
            filteredEcoles(){
                var items = this.books.map(item => item.school).filter((value, index, self) => self.indexOf(value) === index);
                items = items.sort(function (a, b) {
                    return a.localeCompare(b); //using String.prototype.localCompare()
                });
                return items;
            },
            filteredBranches(){
               var items = this.books.map(item => item.branches[0]).filter((value, index, self) => self.indexOf(value) === index);
                items = items.sort(function (a, b) {
                    return a.localeCompare(b); //using String.prototype.localCompare()
                });
                return items;
            },filteredClassDomain(){
                var items = this.books.map(item => item.class[0].class_name).filter((value, index, self) => self.indexOf(value) === index);
                items = items.sort(function (a, b) {
                    return a.localeCompare(b); //using String.prototype.localCompare()
                });
                return items;

            },filteredLevel(){
                var items = this.books.map(item => item.class[0].level).filter((value, index, self) => self.indexOf(value) === index);
                items = items.sort(function (a, b) {
                    return a.localeCompare(b); //using String.prototype.localCompare()
                });
                return items;

            },filteredLivres(){
                var items = this.books.map(item => item.book).filter((value, index, self) => self.indexOf(value) === index);
                items = items.sort(function (a, b) {
                    return a.localeCompare(b); //using String.prototype.localCompare()
                });
                return items;
            },





        },methods:{
            addLivreFilter(){
                return this.filteredSearchedLivres.indexOf(this.livre) === -1 ? this.filteredSearchedLivres.push(this.livre) : console.log("This item already exists");

            }
            ,
            deleteLivreFilter(){
                var index = this.filteredSearchedLivres.indexOf(this.filterLivre);
                return index >= 0 ? this.filteredSearchedLivres.splice(index, 1) : console.log("This item doesn't exist");

            },
            filterLivreOnChange(e){
                this.filterLivre=e.target.value;
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


