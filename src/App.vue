<script>
import AppMain from './components/AppMain.vue';

export default {
  data() {
    return {

    }
  },
  components: {
    AppMain,
  }
}
</script>


<template>
  <nav class="navbar navbar-dark bg-dark px-5">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">
        <h2>Projects For You</h2>
      </a>
    </div>
  </nav>
  <main>
    <AppMain />
  </main>
</template>


<style lang="scss">
@use "./style/general.scss";
</style>