<template>
  <router-view/>
</template>

<script>

</script>

<style>

@font-face{
  font-family: Valkyrie;
  src: url("@/assets/fonts/Valkyrie C4 Regular.otf");
}
@font-face{
  font-family: Valkyrie;
  src: url("@/assets/fonts/Valkyrie C4 Bold.otf");
  font-weight: bold;
}
#app {
  font-family: Valkyrie, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #b3576a;
}
body{
  background:#322646;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
