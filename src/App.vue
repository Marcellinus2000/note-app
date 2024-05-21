<script setup>
import { RouterView } from "vue-router";
import NoteHeader from "./components/Note-Header.vue";
</script>

<template>
  <div>
  <NoteHeader/>
  <router-view/>
  </div>
</template>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@300&display=swap");

* {
  font-family: "Montserrat", sans-serif;
  margin: -10px;
  padding: 0;
  box-sizing: border-box;
}
</style>
