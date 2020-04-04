<script>
	export let id;
	import p5 from "../lib/p5";

	export let sketch;

	import { onMount } from "svelte";

	onMount(function() {
	  let myp5 = new p5(sketch, id);
	});

	const car = {
	  model: "Fiesta",
	  manufacturer: "Ford",
	  fullName: function() {
	    return `${this.manufacturer} ${this.model}`;
	  }
	};

	$: fullName = car.fullName();
</script>

<style>
</style>
<div {id}></div>