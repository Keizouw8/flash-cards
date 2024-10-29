<script>
	import { cards } from "../store.svelte";

	function newCard(i=0){
		cards.splice(i+1, 0, {
			chinese: "",
			pinyin: "",
			english: ""
		});
	}
</script>

<a href="/">Home</a>
<h1>Manage Set</h1>

{#if !cards.length}
	<button onclick={newCard}>New Card</button>
{/if}

{#each cards as card, i}
	<div>
		<input type="text" placeholder="chinese" bind:value={card.chinese}>
		<input type="text" placeholder="pinyin" bind:value={card.pinyin}>
		<input type="text" placeholder="english" bind:value={card.english}>
		<button onclick={() => cards.splice(i, 1)}>remove</button>
		<button onclick={() => newCard(i)}>add below</button>
	</div>
{/each}