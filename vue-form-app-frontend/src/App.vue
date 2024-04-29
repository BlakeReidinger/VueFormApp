<template>
  <div class="header-section">
    <img src="./assets/logo.png" alt="vue_logo" class="header-img" />
    <h1 class="header-title">Vue Form</h1>
    <img src="./assets/logo.png" alt="vue_logo" class="header-img" />
  </div>
  <hr />
  <h2>Create Ticket</h2>
  <VueForm />
</template>

<script>
import VueForm from "./components/VueForm";
import "./App.css";

export default {
  name: "App",
  components: {
    VueForm,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
