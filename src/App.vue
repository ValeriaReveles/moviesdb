<template>
  <router-view/>
</template>

<script>

</script>

<style>

@font-face{
  font-family: Orbitron;
  src: url("@/assets/fonts/Orbitron-Regular.ttf");
}
@font-face{
  font-family: Orbitron;
  src: url("@/assets/fonts/Orbitron-SemiBold.ttf");
  font-weight: bold;
}
#app {
  font-family: BungeeInl, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #b3576a;
}
body{
    background: linear-gradient(to bottom right, #827298, #322646 25%);
	overflow: scroll;
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
