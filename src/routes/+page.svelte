<script lang="ts">
	import Counter from "./Counter.svelte";
	import welcome from "$lib/images/svelte-welcome.webp";
	import welcomeFallback from "$lib/images/svelte-welcome.png";
	import Carousel from "../lib/components/ProjectsAdd/Carousel.svelte";
</script>

<section>
	<Carousel
		initialItems={["Item 1", "Item 2", "Item 3"]}
		title={"Projects"}
	/>
	<Carousel
		initialItems={["Item 1", "Item 2", "Hahahah"]}
		title={"Wichtige Projekte"}
	/>
	<Carousel
		initialItems={["Item 1", "Item 2", "Item 3"]}
		title={"Bald Auslaufend"}
	/>
	<Carousel initialItems={["Item 1", "Item 2", "Item 3"]} />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: left;r;
		align-items: center;
		flex: 0.6;
	}
</style>
