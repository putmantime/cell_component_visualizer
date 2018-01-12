<template>
  <div id="app">
    <cell-comp goTerm="GO:0005794"></cell-comp>
  </div>
</template>
<!--peroxisome: GO:0005777 -->
<!--endosome: GO:0005768-->
<!--golgi: GO:0005794-->
<script>
  import CellComp from './components/CellComp';

  export default {
    name: 'app',
    components: {
      'cell-comp': CellComp,
    },
  };
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
