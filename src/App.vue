<template>
<div><code>
    Bonjour, D'abord, je vous informe que j'ai converti le tableau de donnees data.min.js vers un fichier json(data.json) a travers une fonction que j'ai cree ( voir assets/index.html),
    Cela m'a permis de bien comprendre la structure du fichier ainsi que d'avoir une idee globale afin de creer le systeme de recherche.

    pour les statistiques, j'ai mis en place le nombre de chaque composant(nombre d'ecoles/branches...)

</code></div>
    <DisplayBooks  />
</template>

<script>
   import DisplayBooks from './components/Books.vue';

export default {
  name: 'App',
  components: {
      DisplayBooks
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


input[type=text] {
    width: 80%;
    padding: 5px 10px;
    margin: 5px;
    box-sizing: border-box;
}
select {
    width: 80%;
    padding: 5px 10px;
    margin: 5px;
    border-radius: 5px;
}
</style>
