<template>

  <div class="contain">

    <a id="sair" href="/"><b>Sair</b></a>

    <Categoria :key="categoria.id"
               v-for="categoria in categorias"
               v-bind:titulo="categoria.nome"
               v-bind:filmes="categoria.filmes">
    </Categoria>

  </div>
</template>

<script>


  import Categoria from './components/Categoria'

  export default {
    components: {
      Categoria
    },

    name: 'App',
    data() {
      return {
        categorias: []
      }
    },
    created() {

      this.$http.get('http://localhost:3000/categorias').then(response => {
        this.categorias = response.body;
      });
    }
  }
</script>

<style>
  @import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.css");

  body,
  html {
    background-color: black;
    padding: 0 10px;
    margin: 0;
    min-height: 100vh;
  }
  a {
    color: red;
    text-decoration: none;
    padding-left: 1180px;
  }

  .contain {
    width: 1329px
  }



</style>
