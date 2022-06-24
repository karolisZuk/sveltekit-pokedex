<script>
	import { pokemon } from '../stores/pokestore';
	import PokemanCard from '../components/pokemanCard.svelte';

	let searchTerm = '';
	let filteredPokemon = [];

	$: {
		if (searchTerm) {
			filteredPokemon = $pokemon.filter(
				(pokeman) =>
					pokeman.name.trim().toLowerCase().includes(searchTerm.trim().toLowerCase()) ||
					pokeman.id + ''.trim() === searchTerm.trim()
			);
		} else {
			filteredPokemon = [...$pokemon];
		}
	}
</script>

<svelte:head>
	<title>Svelte Kit Pokedex</title>
</svelte:head>

<h1 class="text-4xl text-center my-8 uppercase">Svelte Kit Pokedex</h1>

<input
	class="w-full rounded-md text-lg p-4 border-2"
	bind:value={searchTerm}
	type="text"
	placeholder="Search Pokemon"
/>

<div class="py-4 grid gap-4 lg:grid-cols-4 md:grid-cols-3 grid-cols-2">
	{#each filteredPokemon as pokeman}
		<PokemanCard {pokeman} />
	{/each}
</div>
