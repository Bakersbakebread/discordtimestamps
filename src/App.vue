<template>
<header>
  <h1>Discord timestamp formatter</h1>
  <p>Choose a date from the picker and have it displayed local to you in Discord</p>
  </header>
<main>
  <Home/>
</main>
</template>

<script>
import Home from "./pages/Home.vue";

export default {
  name: "App",
  components: {
    Home,
  },
};
</script>

<style>
body{
  background: #36393f;
  color: #dcddde;
font-family: 'Roboto', sans-serif;  font-weight: 400;
}
h1, h2, h3{
}
main{
  max-width: 900px;
  margin: 0 auto;
}
header{
    max-width: 900px;
  margin: 0 auto;
  padding-top: 4rem;
  text-align: center;
}
</style>
