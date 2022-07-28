<template>
	<Teleport to="body" v-if="showModal">
		<Modal @close="showModal = false">
			<form>
				<div class="modalForm">
					<br>
					<input v-model="movieTitle.title " type="text" class="write" placeholder="Title">
					<br>
					<input v-model="movieTitle.poster_path " type="text" class="write" placeholder="Poster URL">
					<br>
					<input v-model="movieTitle.overview " type="text" class="write" placeholder="Description">
					<br>
					<input v-model="movieTitle.vote_average " type="text" class="write" placeholder="Movie Rating">
					<br>
					<button class="addButton" @click.prevent="addMovie" >Add Movie</button>
				</div>
			</form>
		</Modal>
	</Teleport>
	<Teleport to="body" v-if="showModalEdit">
		<Modal @close="showModalEdit = false">
			<form>
				<div class="modalForm">
					<br>
					<select @change="selectedMovie(selected)" v-model="selected" class="write" name="movieSelect" id="movieSelect" >
						<option disabled value="">Please Select a Movie to Edit</option>
						<option v-for="(movie, index) in movies.results">{{ movies.results[index].title }}</option>
					</select>
					<br>
					<label for="title">Title</label>
					<input id="title" type="text" class="write" placeholder="Title" v-model="selectedTitle.title">
					<br>
					<label for="posterURL">Poster URL</label>
					<input id="posterURL" type="text" class="write" placeholder="Poster URL" v-model="selectedTitle.poster_path">
					<br>
					<label for="description">Description</label>
					<input id="description" type="text" class="write" placeholder="Description" v-model="selectedTitle.overview">
					<br>
					<label for="rating">Movie Rating</label>
					<input id="rating" type="text" class="write" placeholder="Movie Rating" v-model="selectedTitle.vote_average">
					<br>
					<button class="addButton" @click.prevent="editMovie" >Edit Movie</button>
				</div>
			</form>
		</Modal>
	</Teleport>
	<div class="header-search">
		<h1 class="neon-text">El Tomate Pudrido</h1>
		<button class="addButton" @click="showModalEdit = true">Edit a Movie</button>
		<button class="addButton" @click="showModal = true">Add a Movie</button>
		<input class="search" type="text" v-model="search" @keyup="searchArray" placeholder="Search movies..." />
	</div>
	<suspense>
		<div v-if="error">{{ error }}</div>
	</suspense>
		<div v-if="search === ''" class="card-container">
			<h1>ACTION</h1>
			<div v-for="(movie, index) in movies.results">
				<div v-for="category in movie.genre_ids">
					<div v-if="category === 28">
						<div v-if="index % 2 === 0" :[movie.rendered]="true" class="movie-card" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
							<div class="card-contents">
								<div class="title"><p>{{ movies.results[index].title }}</p></div>
								<p class="overview">{{ movies.results[index].overview }}</p>
								<p class="vote">{{ movies.results[index].vote_average }}</p>
								<button class="deleteButton" @click="deleteParent(index)">X</button>
							</div>
						</div>
						<div v-if="index % 2 !== 0" :ref="movie.rendered = true" class="movie-card1" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
							<div class="card-contents">
								<div class="title"><p>{{ movies.results[index].title }}</p></div>
								<p class="overview">{{ movies.results[index].overview }}</p>
								<p class="vote">{{ movies.results[index].vote_average }}</p>
								<button class="deleteButton" @click="deleteParent(index)" >X</button>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<div v-if="search === ''" class="card-container">
			<h1>COMEDY</h1>
			<div v-for="(movie, index) in movies.results">
				<div v-for="category in movie.genre_ids">
					<div v-if="category === 35">
						<div v-if="index % 2 === 0" class="movie-card" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
							<div class="card-contents">
								<div class="title"><p>{{ movies.results[index].title }}</p></div>
								<p class="overview">{{ movies.results[index].overview }}</p>
								<p class="vote">{{ movies.results[index].vote_average }}</p>
								<button class="deleteButton" @click="deleteParent(index)">X</button>
							</div>
						</div>
						<div v-if="index % 2 !== 0" class="movie-card1" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
							<div class="card-contents">
								<div class="title"><p>{{ movies.results[index].title }}</p></div>
								<p class="overview">{{ movies.results[index].overview }}</p>
								<p class="vote">{{ movies.results[index].vote_average }}</p>
								<button class="deleteButton" @click="deleteParent(index)" >X</button>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<div v-if="search === ''" class="card-container">
			<h1>HORROR</h1>
			<div v-for="(movie, index) in movies.results">
				<div v-for="category in movie.genre_ids">
					<div v-if="category === 27">
						<div v-if="index % 2 === 0" class="movie-card" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
							<div class="card-contents">
								<div class="title"><p>{{ movies.results[index].title }}</p></div>
								<p class="overview">{{ movies.results[index].overview }}</p>
								<p class="vote">{{ movies.results[index].vote_average }}</p>
								<button class="deleteButton" @click="deleteParent(index)">X</button>
							</div>
						</div>
						<div v-if="index % 2 !== 0" class="movie-card1" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
							<div class="card-contents">
								<div class="title"><p>{{ movies.results[index].title }}</p></div>
								<p class="overview">{{ movies.results[index].overview }}</p>
								<p class="vote">{{ movies.results[index].vote_average }}</p>
								<button class="deleteButton" @click="deleteParent(index)" >X</button>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	<div v-if="search === ''" class="card-container">
		<h1>MISCELLANEOUS</h1>
		<div v-for="(movie, index) in movies.results">
					<div class="movie-card" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movies.results[index].poster_path}')`}">
						<div class="card-contents">
							<div class="title"><p>{{ movies.results[index].title }}</p></div>
							<p class="overview">{{ movies.results[index].overview }}</p>
							<p class="vote">{{ movies.results[index].vote_average }}{{ movies.rendered }}</p>
							<button class="deleteButton" @click="deleteParent(index)">X</button>
						</div>
			</div>
		</div>
	</div>
		<div v-else class="card-container">
			<div v-for="(movie, index) in movieSearch">
				<div v-if="index % 2 === 0" class="movie-card" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movieSearch[index].poster_path}')`}">
					<div class="card-contents">
						<div class="title"><p>{{ movieSearch[index].title }}</p></div>
						<p class="overview">{{ movieSearch[index].overview }}</p>
						<p class="vote">{{ movieSearch[index].vote_average }}</p>
						<button class="deleteButton" @click="deleteParentMod(index)">X</button>
					</div>
				</div>
				<div v-else class="movie-card1" :style="{'background-image':`url('https://image.tmdb.org/t/p/original/${movieSearch[index].poster_path}')`}">
					<div class="card-contents">
						<div class="title"><p>{{ movieSearch[index].title }}</p></div>
						<p class="overview">{{ movieSearch[index].overview }}</p>
						<p class="vote">{{ movieSearch[index].vote_average }}</p>
						<button class="deleteButton" @click="deleteParentMod(index)">X</button>
					</div>
				</div>
			</div>
		</div>
</template>

<script>
import { ref } from "vue";
import Modal from "@/components/Modal.vue"
import Loading from "@/views/LoadingPage.vue"
export default {
	name: 'Movies',
	components: { Modal, Loading },
	setup() {
		const movies = ref([]);
		const movies1 = ref([]);
		const movies2 = ref([]);
		const error = ref(null);
		const search = ref("");
		const movieSearch = ref([]);
		const buttonPressed = ref(null)
		const showModal = ref(false)
		const showModalEdit = ref(false)
		const selected = ref("")
		const selectedTitle = ref([])
		const movieTitle = ref({
			title: "",  poster_path: "",  overview: "",  vote_average: ""
		})

		const load = async () => {
			try {
				let data = await fetch('https://api.themoviedb.org/3/discover/movie?api_key=85acbd9e80501242e6970d5c94bf2af3&language=en-US&sort_by=popularity.desc&include_adult=true&include_video=false&page=1&with_watch_monetization_types=flatrate',
					{
						method: 'get',
						headers: {
							'content-type': 'application/json'
						}
					})
				if (!data.ok) {
					throw Error("No data available for the request")
				}
				movies1.value = await data.json();
			} catch (err) {
				error.value = err.message
				console.log(error.value)
			}
			try {
				let data = await fetch('https://api.themoviedb.org/3/discover/movie?api_key=85acbd9e80501242e6970d5c94bf2af3&language=en-US&sort_by=popularity.desc&include_adult=true&include_video=false&page=2&with_watch_monetization_types=flatrate',
					{
						method: 'get',
						headers: {
							'content-type': 'application/json'
						}
					})
				if (!data.ok) {
					throw Error("No data available for the request")
				}
				movies2.value = await data.json();
				console.log(movies2.value);
			} catch (err) {
				error.value = err.message
				console.log(error.value)
			}
			await movieCombine();
		}
		load()

		const movieCombine = async () => {
			console.log("fired");
			movies.value.results = []
			movies.value.page = await movies1.value.page;
			for (let i = 0; i < 20; i++) {
				movies.value.results.push(await movies1.value.results[i])
				movies.value.results.rendered = false;
			}
			for (let i = 0; i < 20; i++) {
				movies.value.results.push(await movies2.value.results[i])
				movies.value.results.rendered = false;
			}
			movies.value.total_pages = await movies1.value.total_pages;
			movies.value.total_results = await movies1.value.total_results

			console.log(movies.value)
			return movies.value
		}

		async function searchArray() {
			movieSearch.value = [];
			for (let i = 0; i < movies.value.results.length; i++) {
				if (movies.value.results[i].title.toLowerCase().indexOf(search.value.toLowerCase()) > -1) {
					movieSearch.value.push(movies.value.results[i]);
				}
				console.log(movies.value)
			}
		}
		const deleteParent = async (i) => {
			movies.value.results.splice(i,1)
		}
		const deleteParentMod = async (i) => {
			movieSearch.value.splice(i,1)
			movies.value.results.forEach(element => {
				if (element.title.toLowerCase === movieSearch.value) {

				}
			})
		}

		const addMovie = () => {
			movies.value.results.push(movieTitle.value)
			showModal.value = false
			console.log(movieTitle.value);
		}
		const selectedMovie = (title) => {
			console.log("fired");
			selectedTitle.value = [];
			for (let i = 0; i < movies.value.results.length; i++) {
				if (movies.value.results[i].title.toLowerCase().indexOf(title.toLowerCase()) > -1) {
					selectedTitle.value = movies.value.results[i];
				}
			}
		}
		const editMovie = () => {
			console.log("You're doing great <3")
			for (let i = 0; i < movies.value.results.length; i++) {
				if (movies.value.results[i].title.toLowerCase().indexOf(selectedTitle.value.title.toLowerCase()) > -1) {
					movies.value.results[i].title = selectedTitle.value.title
					movies.value.results[i].poster_path = selectedTitle.value.poster_path
					movies.value.results[i].overview = selectedTitle.value.overview
					movies.value.results[i].vote_average = selectedTitle.value.vote_average
				}
			}
			showModalEdit.value = false;
		}
		return {
			movies,
			error,
			search,
			movieSearch,
			searchArray,
			buttonPressed,
			deleteParent,
			deleteParentMod,
			showModal,
			showModalEdit,
			movieTitle,
			selected,
			selectedTitle,
			selectedMovie,
			addMovie,
			editMovie
		}
	}
}
</script>

<style scoped>
@font-face {
	font-family: NeoncityDisplay;
	src: url("@/assets/fonts/NeoncityDisplay-MVVLv.otf");
}
@font-face {
	font-family: KdamThmor;
	src: url("@/assets/fonts/KdamThmorPro-Regular.ttf");
}
* {
	box-sizing: border-box;
}
.home {
	overflow: scroll;
	margin: 0;
	padding: 0;
}
.card-container {
	display: flex;
	flex-wrap: wrap;
	flex-direction: column;
	justify-content: center;
	align-items: flex-end;
	height: 550px;
	width: 100%;
	margin: 1em;
	background: linear-gradient(90deg, transparent, rgba(0,0,0,.3) 99%);
	overflow-x: scroll;
	overflow-y: hidden;
}
.card-container h1 {
	font-family: KdamThmor, serif;
	position: relative;
	margin: auto 1em;
}
.movie-card {
	height: 500px;
	width: 300px;
	font-family: HEXCO,sans-serif;
	border-radius: 10px;
	background-size: cover;
	background-repeat: no-repeat;
	margin: .5em;
	box-shadow: #68D9C3 6px 6px 15px ;
	letter-spacing: 2px;
	border: solid 1px #C5FCEF;

}
.movie-card1 {
	height: 500px;
	width: 300px;
	border-radius: 10px;
	background-size: cover;
	margin: .7em;
	box-shadow: #68D9C3 6px 6px 15px;
	font-family: HEXCO,sans-serif;
	letter-spacing: 2px;
	border: solid 1px #C5FCEF;

}
.header-search h1{
	font-size: 3rem;
	padding-bottom: .4em;
	padding-top:.2em;
	text-align: left;
	padding-left: .6em;
	margin: 0 0 0 .7em;
	font-family: NeoncityDisplay, sans-serif;
	color: #fff;
	overflow: visible;
	animation: pulsate 0.11s ease-in-out infinite alternate;
	text-shadow:
		0 0 7px #fff,
		0 0 10px #fff,
		0 0 21px #fff,
		0 0 42px #f09,
		0 0 82px #f09,
		0 0 92px #f09,
		0 0 102px #f09,
		0 0 131px #f09;
}
@keyframes pulsate {
	100% {
		text-shadow: 0 0 4px #fff,
		0 0 11px #fff,
		0 0 19px #fff,
		0 0 40px #f09,
		0 0 80px #f09,
		0 0 90px #f09,
		0 0 100px #f09,
		0 0 130px #f09;
	}
	0% {
		text-shadow: 0 0 4px #fff,
		0 0 10px #fff,
		0 0 18px #fff,
		0 0 38px #f09,
		0 0 73px #f09,
		0 0 80px #f09,
		0 0 94px #f09,
		0 0 120px #f09;
	}
}
.header-search{
	display: flex;
	align-items: center;
	justify-content: space-between;
	background: linear-gradient(90deg, transparent 20%, #1e1432);
}

.title{
	font-family: Orbitron, sans-serif;
	font-weight: bold;
}

.overview{
	font-family: KdamThmor, sans-serif;
}

.search{
	height:2em;
	width: 30em;
	margin:1em;
	background: #faeaff;
	font-family: Orbitron, serif;
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
	margin: auto auto 0;
	height: 3rem;
	width: 80%;
	padding: 10px;
	justify-content: center;
	overflow: hidden;
	border-bottom: #F9F871 1px solid;
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
	display: grid;
	grid-template-areas: "title button" "overview overview" "vote vote";
	grid-template-columns: 1fr 1rem;
	opacity: 0;
	transition: ease-out .7s;
	overflow: scroll;
}
.card-contents:hover {
	opacity: 1;
	background: linear-gradient(160deg, #E68164, #733C61);
	height: inherit;
	border-radius: 10px;
}
.deleteButton {
	grid-area: button;
	background: none;
	border: none;
	position: relative;
	bottom: 1em;
	right: .5em;
	margin: 0;
	padding: 0;
	color: #FFB85E;
	font-size: 1rem;
	transition: 1s ease-in-out;
}
.deleteButton:hover {
	color: #F9F871;
	font-size: 1.2rem;
}
.addButton {
	background: linear-gradient(to bottom right, #B3576A, #E68164);
	border: 0;
	border-radius: 12px;
	color: #FFFFFF;
	cursor: pointer;
	display: inline-block;
	font-family: KdamThmor,serif;
	font-size: 1rem;
	line-height: 2.5;
	outline: transparent;
	padding: 0 1rem;
	margin: 1em auto;
	text-align: center;
	text-decoration: none;
	transition: box-shadow .7s ease-in-out;
	user-select: none;
	-webkit-user-select: none;
	touch-action: manipulation;
	white-space: nowrap;
}
.addButton:not([disabled]):focus {
	box-shadow: 0 0 .25rem rgba(0, 0, 0, 0.5), -.125rem -.125rem 1rem rgba(239, 71, 101, 0.5), .125rem .125rem 1rem rgba(255, 154, 90, 0.5);
}
.addButton:not([disabled]):hover {
	box-shadow: 0 0 .25rem rgba(0, 0, 0, 0.5), -.125rem -.125rem 1rem rgba(239, 71, 101, 0.5), .125rem .125rem 1rem rgba(255, 154, 90, 0.5);
}
.write {
	font-family: Orbitron, serif;
	font-size: .8rem;
	color: #eee;
	background: #1E1432;
	border: none;
	width: 80%;
	height: 2rem;
	margin: 1em;
	padding-left: 1em;
	border-radius: 20px;
	transition: ease-in-out 1.3s linear;
}
.write:active, .write:focus {
	outline: none;
	border-bottom: #E68164 2px solid;
	transition: ease-in-out 1.3s linear;
}
.write::placeholder {
	color: #ddd;
}
label {
	font-family: Orbitron, serif;
	font-size: 1rem;
	color: #eee;
	margin-left: 1em;
}
.modalForm {
	display: grid;
	justify-content: center;
	grid-template-columns: 1fr;
}
</style>
