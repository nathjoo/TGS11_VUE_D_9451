<template>
  <v-app>
    <main>
      <router-view></router-view>
    </main>
  </v-app>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style lang="scss">
  main{
    background-image: url('./assets/kotak.png');
    background-size: cover;
  }
</style>
