<script lang="ts">
	import './main.css';
	import duck from '$lib/assets/duck.mp4';
</script>

<main class="relative h-screen bg-white overflow-hidden">
	<video autoplay playsinline loop class="w-full h-full object-contain mx-auto mask-blur">
		<track kind="captions" />
		<source src={duck} type="video/mp4" />
	</video>
</main>

<style>
	/* Add Tailwind CSS classes directly in the style section */
	video {
		@apply w-full h-full object-contain mx-auto;
	}

	.mask-blur {
		/* Apply a gradient mask to create a blur effect at the edges */
		mask-image: linear-gradient(to bottom, transparent 0%, white 5%, white 95%, transparent 100%);
	}
</style>
