<script lang="ts">
	import './main.css';
	import duck from '$lib/assets/duck.mp4';
	import { onMount } from 'svelte';

	let videoSrc = duck;
	let video: any;
	let volume: any;
	let show_button = false;
	let erenabled = false;
	let button_title = 'Toggle Earrape!?';

	onMount(async () => {
		video = document.getElementById('video');
		addEventListener('ended', () => {
			video.currentTime = 0; // Rewind to the beginning
			video.play();
		});

		// Start playing the video if it's not started
		if (video.paused) {
			video.play();
		}

		// Start playing the video when the screen is clicked
		video.addEventListener('click', () => {
			if (show_button) {
				show_button = false;
			} else {
				show_button = true;
			}
			if (video.paused) {
				video.play();
			} else {
				video.play();
			}
		});
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

	function amplifyMedia(mediaElem: any, multiplier: number) {
		var context = new (window.AudioContext || window.webkitAudioContext)(),
			result = {
				context: context,
				source: context.createMediaElementSource(mediaElem),
				gain: context.createGain(),
				media: mediaElem,
				amplify: function (multiplier: number) {
					result.gain.gain.value = multiplier;
				},
				getAmpLevel: function () {
					return result.gain.gain.value;
				}
			};
		result.source.connect(result.gain);
		result.gain.connect(context.destination);
		result.amplify(multiplier);
		return result;
	}

	function handleButtonClick() {
		if (erenabled) {
			button_title = 'Lmao, nope';
		} else {
			if (video) {
				amplifyMedia(video, 100);
				erenabled = true;
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

	{#if show_button}
		<!-- Your overengineered button -->
		<div class="fixed bottom-4 right-4">
			<button
				on:click={handleButtonClick}
				class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
			>
				{button_title}
			</button>
		</div>
	{/if}
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
