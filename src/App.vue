<template>
  <div id="app">
    <h2 class="main-title">Valoraciones del producto</h2>
    <p class="main-description">
      Aquí puedes consultar las últimas valoraciones que los usuarios han hecho
      sobre este producto.
    </p>
    <ValorationsContainer />
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
    ValorationsContainer: () => import('@/containers/Valorations.vue')
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  .main {
    &-title {
      color: #359436;
    }
    &-description {
      margin-top: 0;
    }
  }
}
</style>
