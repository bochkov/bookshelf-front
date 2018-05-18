<template>
    <div id="app">
        <!--<img src="./assets/logo.png">-->
        <h3>Книжная полка</h3>
        <Search />
    </div>
</template>

<script>
import Search from "./components/Search";

export default {
  name: "app",
  components: {
    Search
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Playfair+Display");
#app {
  font-family: "Playfair Display", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

h3 {
  text-align: center;
}
</style>