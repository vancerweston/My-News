<template>
  <div id="app">
    <div class="navBar">
      <div class="title">
        <img src="../src/assets/logo.png" alt="" />
      </div>
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
  background-color: white;
  color: white;
  padding: 10px 16px;
  text-decoration: none;
  text-align: center;
}
img {
  height: 100px;
}
</style>
