<template>
       <searchComponentCheck v-on:searchQuery="setSearchQuery($event)" v-on:check-box-state="setSearchQueryCheck($event)" title="Search" v-model="searchQuery"  /><br>
       <selectComponentCheck v-on:check-box-state="setEcoleCheck($event)" v-on:selected-value="setEcoleValue($event)" title="Ecole" v-model="ecole" :lst_options="filteredEcoles"/><br>
       <selectComponentCheck v-on:check-box-state="setBrancheCheck($event)" v-on:selected-value="setBrancheValue($event)" title="branche" v-model="branche" :lst_options="filteredBranches"/><br>
       <selectComponentCheck v-on:check-box-state="setClassDomainCheck($event)" v-on:selected-value="setClassDomainValue($event)" title="classDomain" v-model="classDomain" :lst_options="filteredClassDomain"/><br>
       <selectComponentCheck v-on:check-box-state="setLevelCheck($event)" v-on:selected-value="setLevelValue($event)" title="level" v-model="level" :lst_options="filteredLevel"/><br>
        <selectBooksComponent v-on:selected-value="setLivreValue($event)" title="Livre" v-model="livre" :lst_options="filteredLivres"/><br>
<b>Trier par Niveau de Classe/Domaine?</b>
    <input type="checkbox" @click="checkSortClassDomain=!checkSortClassDomain">
    <div v-if="filteredBooks.length"><b>Sorted Length = {{ filteredBooks.length }}</b></div><br>
           <div v-for="book in filteredBooks" :key="book" style="">
               <BookElement :book="book"/>
           </div>
    <input type="button" value="Recherche" onclick="search();">
</template>

<!--       <input class="form-control" type="text" v-model="searchQuery" placeholder="Search" /><br>-->

<!--       <b>Branche : </b><br>-->
<!--       <SelectComponent v-model="branche" :options="filteredBranches"/><br>-->

<!--       <b>classDomain : </b><br>-->
<!--       <SelectComponent v-model="classDomain" :options="filteredClassDomain"/><br>-->

<!--       <b>level : </b><br>-->
<!--       <SelectComponent v-model="level" :options="filteredLevel"/><br>-->

<!--       <b>Livres : </b><br>-->
<!--       <SelectComponent v-model="livre" :options="filteredLivres"/>-->

<!--       <br><button class="btn" v-on:click="addLivreFilter">add</button><button v-on:click="deleteLivreFilter" class="btn">delete</button><br>-->

<!--       <SelectComponent v-model="filterLivre" @change="filterLivreOnChange($event)" :options="filteredSearchedLivres" multiple="true"/>-->

<script>

    import _data from "../assets/data.json";
    import BookElement from "./BookElement.vue";
     import selectComponentCheck from "./SelectComponentCheck.vue";
    import searchComponentCheck from "./searchComponentCheck.vue";
    import selectBooksComponent from "./selectBooksComponent.vue";

    // SelectComponent

    export default {
        name: 'DisplayBooks',
        components:
            {
                BookElement,
                selectComponentCheck,
                searchComponentCheck,
                selectBooksComponent
            },
        data() {

            return {
                books: _data,

                //store searched words
                searchQuery:'',
                //is activated
                isSearchQuery:false,

                ecole:'',
                isEcole:false,

                branche:'',
                isBranche:false,

                classDomain:'',
                isClassDomain:false,

                level:'',
                isLevel:false,

                filteredSearchedLivres: [],
                isFilteredSearchedLivres: false,

                filterLivre: '',
                isFilterLivre: false,

                checkSortClassDomain : false,



                localStorageData:{},

            };
        },

        watch: {
            pref:function(){


            }
        },
        computed: {

            //this is the main function to filter the data based on all activated criteria...
            filteredBooks (){
                var result;
               //storing
                // if(localStorage.getItem("result") === null || JSON.parse(localStorage.getItem("result")).length<1){
                //     result =  this.books;
                // }else{
                //     result = JSON.parse(localStorage.getItem("result"));
                // }

                result =  this.books;

                //console.log(SelectComponent.props.options);

                //checking if the search bar contains something
                if(this.searchQuery && this.isSearchQuery){
                    result= this.books.filter((item)=>{
                        return item.name.toLowerCase().includes(this.searchQuery.toLowerCase());
                    })
                }
                //checking if the school has been selected
                if(this.ecole && this.isEcole){
                    result= result.filter((item)=>{
                        console.log("================> "+item.school);
                        return item.school.toLowerCase().includes(this.ecole.toLowerCase());
                    })
                }

                //checking if the branche has been selected
                if(this.branche &&  this.isBranche){
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
                if(this.classDomain &&  this.isClassDomain){
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
                }else if(this.level &&  this.isLevel){
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

                if(this.filterLivre.length>0){
                    result= result.filter((item)=>{
                        for(var i=0; i< this.filterLivre.length; i++){
                            if(item.book == this.filterLivre[i]){
                                return item;
                            }
                        }
                    });
                }

                if(this.checkSortClassDomain){
                         result.sort(function(a, b) {
                            return a.class[0] > b.class[0];
                        });




                }


                localStorage.setItem('result', JSON.stringify(result));

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
            },
            // Define method that will use the payload(searchStr) to update the data property
            setSearchQuery: function(searchStr) {
                this.searchQuery = searchStr.query;
                //SAVING SETTING TO THE LOCAL STORAGE
                this.localStorageData.searchQuery = this.searchQuery;
                localStorage.setItem('localStorageData',JSON.stringify(this.localStorageData));
            },
            setSearchQueryCheck(check) {
                this.isSearchQuery = check.isChecked;
                this.localStorageData.isSearchQuery = this.isSearchQuery;
                localStorage.setItem('localStorageData',JSON.stringify(this.localStorageData));
            },
            setEcoleCheck: function(payload) {
                this.isEcole = payload.isChecked;
                this.localStorageData.isEcole = this.isEcole;
                localStorage.setItem('localStorageData',JSON.stringify(this.localStorageData));
            },
            setEcoleValue: function(payload) {
                this.ecole = payload.selected_option;
                this.localStorageData.ecole = this.ecole;
                localStorage.setItem('localStorageData',JSON.stringify(this.localStorageData));
            },



            setBrancheCheck: function(payload) {
                this.isBranche = payload.isChecked;
                this.localStorageData.isBranche = this.isBranche;
                localStorage.setItem('localStorageData',JSON.stringify(this.localStorageData));
            },
            setBrancheValue: function(payload) {
                this.branche = payload.selected_option;
                this.localStorageData.branche = this.branche;
                localStorage.setItem('localStorageData',JSON.stringify(this.localStorageData));
            },

            setClassDomainCheck: function(payload) {
                this.isClassDomain = payload.isChecked;
                this.localStorageData.isClassDomain = this.isClassDomain;
                localStorage.setItem('localStorageData',JSON.stringify(this.localStorageData));
            },
            setClassDomainValue: function(payload) {
                this.classDomain = payload.selected_option;
                this.localStorageData.classDomain = this.classDomain;
                localStorage.setItem('localStorageData',JSON.stringify(this.localStorageData));
            },

            setLevelCheck: function(payload) {
                this.isLevel = payload.isChecked;
                this.localStorageData.isLevel = this.isLevel;
                localStorage.setItem('localStorageData',JSON.stringify(this.localStorageData));
            },
            setLevelValue: function(payload) {
                this.level = payload.selected_option;
                this.localStorageData.level = this.level;
                localStorage.setItem('localStorageData',JSON.stringify(this.localStorageData));
            },

            setLivreValue: function(payload) {
                 this.filterLivre = payload.selected_options;
                this.localStorageData.filterLivre = this.filterLivre;
                localStorage.setItem('localStorageData',JSON.stringify(this.localStorageData));
            }
        },


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


