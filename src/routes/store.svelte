<script module>
    import { persistedState } from "svelte-persisted-state";
	const cardsStore = persistedState("cards", []);
	export let cards = cardsStore.value;
</script>