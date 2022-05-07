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
.btn {
    display: inline-block;
    font-weight: 400;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    border: 1px solid transparent;
    padding: 0.375rem 0.75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: 0.25rem;
    transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
    margin: 5px;
}
.btn-primary {
    color: #fff;
    background-color: #007bff;
    border-color: #007bff;
}
.btn-danger {
    color: #fff;
    background-color: #dc3545;
    border-color: #dc3545;
}
.btn-warning {
    color: #212529;
    background-color: #ffc107;
    border-color: #ffc107;
}
.btn-success {
    color: #fff;
    background-color: #28a745;
    border-color: #28a745;
}

</style>
