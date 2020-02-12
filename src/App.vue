<template>
  <div id="main" class="container mt-3">
    <cabecalho></cabecalho>
    <lembrete></lembrete>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css"
import "font-awesome/css/font-awesome.css"

// importando componente...
import cabecalho from "./components/cabecalho"
import lembrete from "./components/lembrete"
export default {
  name: 'app',
  components: {
    cabecalho,
    lembrete,
  },  
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Titillium+Web&display=swap');
body{
  background: #f3f3f3;
  font-family: 'Titillium Web', sans-serif;
}
</style>
