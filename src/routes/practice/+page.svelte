<script>
	import { cards } from "../store.svelte";
	let left = [...cards];
	
	let shown = 0;
	let show = false;
	
	let fromChinese = true;
	let fromPinyin = true;
	let fromEnglish = true;
	
	let chinese = "";
	let pinyin = "";
	let english = "";


	function onKeyDown(e){
		if(e.key == "ArrowRight"){
			show = false;

			var canFrom = `${+fromChinese}${+fromPinyin}${+fromEnglish}`.split("").map((v, i) => +v ? i : null).filter(v => v != null);
			shown = canFrom[Math.floor(Math.random() * canFrom.length)];

			var index = Math.floor(Math.random() * left.length);
			chinese = left[index].chinese;
			pinyin = left[index].pinyin;
			english = left[index].english;
			
			left.splice(index, 1);
			if(!left.length) left = [...cards];
		}
		if(e.key == " ") show = !show;
	}
</script>
<a href="/">Home</a>
<h1>Practice Set</h1>
<p>chinese</p><input type="checkbox" bind:checked={fromChinese}>
<p>pinyin</p><input type="checkbox" bind:checked={fromPinyin}>
<p>english</p><input type="checkbox" bind:checked={fromEnglish}>

{#if shown == 0 || show}
	<h2>chinese: {chinese}</h2>
{/if}
{#if shown == 1 || show}
	<h2>pinyin: {pinyin}</h2>
{/if}
{#if shown == 2 || show}
	<h2>english: {english}</h2>
{/if}
<svelte:window on:keydown|preventDefault={onKeyDown} />