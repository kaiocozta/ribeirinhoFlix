<template>

  <div class="gui-card"  v-on:click="exibir=!exibir" >

    <div class="gui-card__media">

      <img v-if="!exibir" class="gui-card__img" v-bind:src="imagem"/>

      <iframe class="gui-card__img" v-if="exibir" v-on:mouseout="exibir=!exibir" :src="url" allowfullscreen></iframe>

    </div>

    <!--    <div class="gui-card__details">-->
    <!--      <div class="gui-card__title">-->
    <!--        {{nomeFilme}}-->
    <!--      </div>-->
    <!--    </div>-->

  </div>
</template>

<script>
  export default {
    name: "Filme",
    props: ['nomeFilme', 'imagem', 'url'],
    data() {
      return {
        exibir: false
      }
    }
  }
</script>

<style scoped>

</style>
