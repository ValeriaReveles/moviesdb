<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <button @click="alertButton">Click Me</button>
	  <Posts />
  </div>
</template>

<script>
import Posts from '@/components/Movies.vue'

export default {
  name: 'HomeView',
	components: {
		Posts
	},
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