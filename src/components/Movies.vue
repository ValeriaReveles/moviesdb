<template>
	<h1>Vue 3 and Fetch Example</h1>
	<div v-if="error">{{ error }}</div>

		<div v-for="(movie, index) in movies" :key="index.results">
			<div class="movie-card"><p>{{ movie.original_title }}</p></div>
		</div>

</template>

<script>
import { ref, onMounted } from "vue";
export default {
	name: 'Movies',
	props: {
	},
	setup() {
		const movies = ref([]);
		// const loading = ref(true);
		const error = ref(null);

		const load = async () => {
			// loading.value = true;
			try {
				let data = await fetch('https://api.themoviedb.org/3/discover/movie?api_key=85acbd9e80501242e6970d5c94bf2af3&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1&with_watch_monetization_types=flatrate',
					{
						method: 'get',
						headers: {
							'content-type': 'application/json'
						}
					})
				if (!data.ok) {
					throw Error("No data available for the request")
				}
				movies.value = await data.json()
				console.log(movies.value)
			} catch (err) {
				error.value = err.message
				console.log(error.value)
			}
		}
	load()
		return {movies, error}
	}
}
</script>