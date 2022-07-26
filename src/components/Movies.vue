<template>
	<div class="header-search">
		<h1>El Tomate Pudrido</h1>
		<input class="search" type="text" v-model="search" placeholder="Search movies..." />
	</div>
	<div v-if="error">{{ error }}</div>
	<div v-if="movies.length === 0"><h1>LOADING...</h1></div>
	<div v-if="search === ''" class="card-container">
		<div v-for="(movie, index) in movies.results">
			<div v-if="index % 2 === 0" class="movie-card" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
				<p ref="movieResult">{{ movies.results[index].title }}</p>
			</div>
			<div v-if="index % 2 !== 0" class="movie-card1" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
				<p ref="movieResult">{{ movies.results[index].title }}</p>
			</div>
		</div>
	</div>
	<div v-else class="card-container">
		<div v-for="(movie, index) in movieSearch">
			<div v-if="movies.results[index].title.toLowerCase().includes(search.toLowerCase())" >
				<div v-if="index % 2 === 0" class="movie-card" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
					<p ref="movieResult">{{ movies.results[index].title }}</p>
				</div>
				<div v-else class="movie-card1" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
					<p ref="movieResult">{{ movies.results[index].title }}</p>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import { ref, computed } from "vue";
export default {
	name: 'Movies',
	setup() {
		const movies = ref([]);
		const error = ref(null);
		const search = ref("");
		const movieSearch = ref([]);
		const load = async () => {
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
				console.log(movies.value);
			} catch (err) {
				error.value = err.message
				console.log(error.value)
			}
		}
		load()
		function searchArray() {
			for (let i = 0; i < movies.value.length; i++) {
				if (movies.results[i].search(search) > -1) {
					movieSearch.value.push(movies.results[i]);
				}
			}
		}
		return {movies, error, search, movieSearch, searchArray}
	}
}
</script>

<style scoped>
.card-container {
	display: flex;
	flex-wrap: wrap;
	flex-direction: row;
	justify-content: space-evenly;
	align-items: center;
	height: 100vh;
	width: 100vw;
	overflow: scroll;
}
.movie-card {
	height: 500px;
	width: 300px;
	border-radius: 10px;
	background-size: cover;
	background-repeat: no-repeat;
	margin: .5em;
	box-shadow: #68D9C3 6px 6px 15px ;
}
.movie-card1 {
	height: 400px;
	width: 300px;
	border-radius: 10px;
	background-size: cover;
	margin: .7em;
	box-shadow: #68D9C3 6px 6px 15px;
}
.header-search h1{
	font-size: 3rem;
	padding-bottom: .4em;
	padding-top:.2em;
	text-align: left;
	padding-left: .6em;
	background: #1e1432;
	margin: 0;
}
.header-search{
	display: flex;
	align-items: center;
	justify-content: space-between;
	background: #1e1432;
}
.search{
	height:2em;
	width: 30em;
	margin:1em;
	background: #faeaff;
	font-family: Valkyrie, serif;
	border: none;
	border-radius: 5px;
	color: #733C61;
}
.search:before, .search:after, .search:active, .search:focus {
	border: none;
}
.search::placeholder {
	color: #733C61;
}
</style>