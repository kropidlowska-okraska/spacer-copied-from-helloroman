<template>
  <div class="app">
    <div class="nav">
      <router-link to="/">spacer</router-link>
      <router-link to="about">about</router-link>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Varela+Round&display=swap');

  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body {
    font-family: 'Varela Round', sans-serif;
    padding: 0;
    margin: 0;
  }

  .nav {
    display: none;
  }
</style>
