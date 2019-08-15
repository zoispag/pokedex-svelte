<script>
  import { onMount } from 'svelte';
  import Type from "./Type.svelte";

  export let pokeid;

  $: pokeUrl = `https://pokeapi.co/api/v2/pokemon/${pokeid}`;

  let pokemonData = {};
  let loaded = false;
  onMount(async () => {
	const res = await fetch(pokeUrl);
    pokemonData = await res.json();
    loaded = true;
  });

  $: typesArray = JSON.stringify(pokemonData) === JSON.stringify({})
    ? []
    : pokemonData.types.slice().sort((a, b) => (a.slot > b.slot) ? 1 : ((b.slot > a.slot) ? -1 : 0))

  function capitalize(val) {
    if (!val) return ''
    val = val.toString()
    return val.charAt(0).toUpperCase() + val.slice(1)
  }
</script>

<style>
  /* Something to make it look pretty */
</style>

{#if loaded}
	<div class="w-1/6 p-8">
        <div class="whitespace-no-wrap text-center">
            (#{ pokemonData.id }) <span class="font-bold">{ capitalize(pokemonData.name) }</span>
        </div>
        <div class="mx-auto w-full">
            <img 
                class="w-full"
                alt={pokemonData.name}
                src={pokemonData.sprites.front_default}
            />
        </div>
        <div class="flex">
            {#each typesArray as {type}, i}
                <Type type={type} />
            {/each}
        </div>
    </div>
{/if}
