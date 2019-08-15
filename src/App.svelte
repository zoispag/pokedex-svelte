<script>
	import Pokemon from "./Pokemon.svelte";

	let maxCount = 50;

	function loadMore() {
		maxCount += 50;
	}

	$: idsList = Array.from(Array(maxCount).keys());
</script>

<div id="app">
    <div class="flex mx-auto max-w-full w-screen flex-wrap">
		{#each idsList as {j}, i}
			<Pokemon pokeid={i+1} />
		{/each}
    </div>
    <div class="flex mx-auto">
		<button
			class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
			on:click={loadMore}
		>Load more { maxCount }</button>
    </div>
</div>
