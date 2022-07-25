<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <button @click="alertButton">Click Me</button>
  </div>
</template>

<script>

export default {
  name: 'HomeView',
  setup () {
	function alertButton() {
		console.log("You clicked me")
	  }
	  return { alertButton }
  }
}
</script>

<style scoped>

</style>