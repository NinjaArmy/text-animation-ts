<template>
  <div id="app">
    <div id="nav">
      <Text-animation></Text-animation>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
<script>
import Vue from "vue";
import { Component } from "vue-class-component";
import TextAnimation from "@/components/TextAnimation";
export default {
  components: { TextAnimation }
};
</script>
