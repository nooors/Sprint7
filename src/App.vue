<template>
  <div id="app">
    <b-container class="app">
      <b-row align-h="start">
        <b-col>
          <div id="nav">
            <router-link :to="{ name: 'Welcome' }">Welcome</router-link>
          </div>
        </b-col>
      </b-row>
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
    max-width: 35%;
  }
}

#nav {
  padding: 3px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
