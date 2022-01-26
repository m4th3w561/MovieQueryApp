<script context="module">
	export async function load({ fetch, params }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/search/movie?api_key=${import.meta.env.VITE_KEY}&language=en-US&query=${params.id}&page=1&include_adult=false`
		);
		const searchedMovie = await res.json();
		// console.log(searchedMovie)
		if (res.ok) {
			return {
				props: { searchedMovie: searchedMovie.results }
			};
		}
	}
</script>

<script>
	import MovieCard from '../../components/MovieCard.svelte';
	export let searchedMovie;
	import { fly } from 'svelte/transition';
</script>

<div
	in:fly={{ y: 50, duration: 500, delay: 500 }}
	out:fly={{ duration: 500 }}
	class="searched-movies"
>
	{#each searchedMovie as movie}
		<MovieCard {movie} />
	{/each}
</div>

<style>
	.searched-movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		grid-column-gap: 1rem;
		grid-row-gap: 2rem;
	}
</style>
