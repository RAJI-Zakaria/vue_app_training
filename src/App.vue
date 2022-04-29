<template>

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
