<template>
  <div class="home">
	  <Movies />
  </div>
</template>

<script>
import Movies from '@/components/Movies.vue'

export default {
  name: 'HomeView',
	components: {
		Movies
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