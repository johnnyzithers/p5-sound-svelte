<script>
	export let id;
	import p5 from "../lib/p5";

	export let sketch;

	import { onMount } from "svelte";

	onMount(function() {
	  let myp5 = new p5(sketch, id);
	});

</script>

<style>
	div { margin: auto; width: 50%; }
</style>
<div {id}></div>