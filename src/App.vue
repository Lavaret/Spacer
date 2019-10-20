<template>

<div id="app">
    <div class="nav">
        <router-link to="/">spacer</router-link>
    </div>
    <router-view />
</div>

</template>

<style lang="css">
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,700&display=swap');

  * {
    box-sizing: border-box;
  }

  body {
    font-family: "Montserrot", sans-serif;
  }
</style>
