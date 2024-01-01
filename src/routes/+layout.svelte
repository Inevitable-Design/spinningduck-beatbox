<script lang="ts">
	import './main.css';
	import duck from '$lib/assets/duck.mp4';
	import { onMount } from 'svelte';

	let videoSrc = duck;
	let video: any;

	onMount(async () => {
		video = document.getElementById('video');

		// Ensure the video keeps playing
		video.addEventListener('ended', () => {
			video.currentTime = 0; // Rewind to the beginning
			video.play();
		});

		// Start playing the video if it's not started
		if (video.paused) {
			video.play();
		}

		// Start playing the video when the screen is clicked
		video.addEventListener('click', () => {
			if (video.paused) {
				video.play();
			} else {
				video.play();
			}
		});
		play();
	});

	async function play() {
		await new Promise((resolve) => setTimeout(resolve, 1000));
		video.play();
	}

	$: {
		if (video) {
			play();
			if (video.paused) {
				video.play();
			}
		}
	}
</script>

<main class="relative h-screen bg-white overflow-hidden">
	<video
		id="video"
		autoplay
		playsinline
		loop
		class="w-full h-full object-contain mx-auto mask-blur video"
	>
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
