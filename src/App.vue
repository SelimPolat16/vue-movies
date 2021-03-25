<template>
  <div class="app">
    <Header>
   <h1>Vue<span> Movies</span></h1>

	<form  @submit.prevent="SearchMovies()"  class="search-box">
			<input type="search"
			class="search-field"
			placeholder="Search for a movie..."
			required
			v-model="search"
		  />
		</form>

    </Header>

		<main>
			<div class="cards"  >
				<Card
				v-for="movie in movies"
				:key="movie.imdbID"
				:movie="movie"
				 />
			</div>
		</main>


  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js'

import Card from './components/Card';

export default {


	setup() {
		const search = ref("");
		const movies = ref([]);


		const SearchMovies =  () => {
			if(search.value != "") {
				fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
					.then(response => response.json())
				.then(data => {
					movies.value = data.Search;
					search.value = "";
			});


			}
		}
		return {
			Card,
			search,
			movies,
			SearchMovies
		}
	}
}
</script>

<style lang="scss">
@import url('//db.onlinewebfonts.com/c/f56a112e86dc5e2699df2b2cd9dfb95e?family=Fontself');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fontself", sans-serif;
  background-color: #141313;

}

Header{
  text-align: center;
  align-items: center;
  margin-right: 30px;
  margin-left: 30px;
  font-size: 30px;

  h1{
    color: #41B883;

     span{
       color: #35495E;
     }
  }

  .search-box{
	   display: flex;
	   justify-content: center;
	   padding-left: 30px;
	   padding-right: 30px;

	   .search-field {
		   appearance: none;
		   background: none;
		   border: none;
		   outline: none;

		   background-color: 	#41B883;
		   box-shadow: 0px 4px 4px rgba(36, 34, 34, 0.15);
		   display: block;
		   width: 100%;
		   max-width: 600px;
		   padding: 15px;
		   border-radius: 20px;
		   color: #0b0b0b;
		   font-size: 20px;
		   transition: 0.6s;

		   &::placeholder{
			   color: 	#fff;
		   }

		  &:focus, &:valid {
			  color: #fff;
			  background-color: #35495E;
			 box-shadow: 0px 8px 8px rgba(143, 137, 137, 0.15);
		  }

	   }
   }




}

main{
	max-width: 1200px;
	margin: 0 auto;
	padding-left: 30px;
	padding-right: 30px;

	.cards{
		display: flex;
		flex-wrap: wrap;
		margin: 0 -8px;
	}
}

</style>
