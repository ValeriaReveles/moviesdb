<template>
  <div class="header-search">
    <h1>El Tomate Pudrido</h1>
    <input class="search" type="text" v-model="input" placeholder="Search movies..." />
  </div>
	<div v-if="error">{{ error }}</div>
	<div v-if="movies.length === 0"><h1>LOADING...</h1></div>
	<div class="card-container">
		<div v-for="(movie, index) in movies.results">
			<div v-if="index % 2 === 0" class="movie-card" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
				<p>{{ movies.results[index].title }}</p>
			</div>
			<div v-if="index % 2 === 1" class="movie-card1" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
				<p>{{ movies.results[index].title }}</p>
			</div>
		</div>
	</div>
</template>

<script>
import { ref, onMounted } from "vue";
export default {
	name: 'Movies',
	setup() {
		const movies = ref([]);
		const error = ref(null);

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
		return {movies, error}
	}
}
</script>

<style scoped>
    .card-container {
	    display: flex;
	    flex-wrap: wrap;
	    flex-direction: row;
	    justify-content: space-around;
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
		margin: .5em;
    box-shadow: #334a52 12px 12px 15px ;
	}
	.movie-card1 {
		height: 400px;
		width: 300px;
		border-radius: 10px;
		background-size: cover;
		margin: .7em;
    box-shadow: #334a52 10px 10px 15px;
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
    font-family: Valkyrie;
    border: none;
    border-radius: 5px;

  }
</style>