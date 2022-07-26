<template>
	<div class="header-search">
		<h1>El Tomate Pudrido</h1>
		<input class="search" type="text" v-model="search" @keyup="searchArray" placeholder="Search movies..." />
	</div>
	<div v-if="error">{{ error }}</div>
	<div v-if="movies.length === 0"><h1>LOADING...</h1></div>
	<div v-if="search === ''" class="card-container">
		<div v-for="(movie, index) in movies.results">
			<div v-if="index % 2 === 0" class="movie-card" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
				<div class="card-contents">
					<div class="title"><p>{{ movies.results[index].title }}</p></div>
					<p class="overview">{{ movies.results[index].overview }}</p>
					<p class="vote">{{ movies.results[index].vote_average }}</p>
				</div>
			</div>
			<div v-if="index % 2 !== 0" class="movie-card1" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
				<div class="card-contents">
					<div class="title"><p>{{ movies.results[index].title }}</p></div>
					<p class="overview">{{ movies.results[index].overview }}</p>
					<p class="vote">{{ movies.results[index].vote_average }}</p>
				</div>
			</div>
		</div>
	</div>
	<div v-else class="card-container">
		<div v-for="(movie, index) in movieSearch">
				<div v-if="index % 2 === 0" class="movie-card" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movieSearch[index].poster_path}')`}">
					<div class="title"><p>{{ movieSearch[index].title }}</p></div>
					<p class="overview">{{ movieSearch[index].overview }}</p>
					<p class="vote">{{ movieSearch[index].vote_average }}</p>
				</div>
				<div v-else class="movie-card1" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movieSearch[index].poster_path}')`}">
					<div class="title"><p>{{ movieSearch[index].title }}</p></div>
					<p class="overview">{{ movieSearch[index].overview }}</p>
					<p class="vote">{{ movieSearch[index].vote_average }}</p>
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
		async function searchArray() {
			movieSearch.value = [];
			for (let i = 0; i < movies.value.results.length; i++) {
				if (movies.value.results[i].title.toLowerCase().indexOf(search.value.toLowerCase()) > -1) {
					movieSearch.value.push(movies.value.results[i]);
				}
			}
			console.log(movieSearch.value)
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
	display: grid;
	grid-template-areas: "vote" "overview" "title";
	height: 500px;
	width: 300px;
	border-radius: 10px;
	background-size: cover;
	background-repeat: no-repeat;
	margin: .5em;
	box-shadow: #68D9C3 6px 6px 15px ;
}
.movie-card1 {
	display: grid;
	grid-template-areas: "vote" "overview" "title";
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
	outline: none;
	color: #733C61;
}
.search:before, .search:after, .search:active, .search:focus {
	border: none;
	outline: none;
}
.search::placeholder {
	color: #733C61;
}
.title {
	grid-area: title;
	position: relative;
	background-color: #F9F871;
	margin: auto auto 0;
	height: 3rem;
	width: 80%;
	padding: 10px;
	justify-content: center;
	border-radius: 2px;
	overflow: hidden;
}
.title p {
	font-size: 1.5rem;
	color: #3a3a3a;
	margin: 0;
	padding: 0;
}
.overview {
	grid-area: overview;
	color: #3a3a3a;
	padding: 1em;
	font-size: 1rem;
}
.vote {
	display: flex;
	position: relative;
	grid-area: vote;
	color: #3a3a3a;
	font-size: 1.5rem;
	background-color: #F9F871;
	border-radius: 50%;
	width: 2em;
	height: 2em;
	justify-content: center;
	align-items: center;
	margin: .2em auto;
	padding: 0;
}
.card-contents {
	opacity: 0;
	transition: ease-in-out .7s;
	overflow: scroll;
}
.card-contents:hover {
	opacity: 1;
	background: linear-gradient(160deg, #E68164, #733C61);
	height: inherit;
	border-radius: 10px;
}
</style>