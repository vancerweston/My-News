<template>
  <div id="app">
    <div class="navBar">
      <h2>MEMBER SPACE</h2>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
  * {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
  }
  body {
    background-color: lightgrey;
  }
  .navBar {
    background-color: #333;
    color: white;
    padding: 10px 16px;
    text-decoration: none;
  }
</style>


