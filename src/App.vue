<template>
  <div id="app">
    <b-container class="app">
      <b-row>
        <router-view :key="$route.path" />
      </b-row>
    </b-container>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  .container.app {
    max-width: 70%;
  }
}

</style>
