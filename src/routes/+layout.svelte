<script>
	import { onMount } from 'svelte';
	import '../app.css';

	let { children, data } = $props();

	// Playlist: [Video ID, Playback Duration (s), Start Time (s)]
	const playlist = [
		{ id: 'BpXlJnRw3OY', duration: 60, start: 10 }, // Peaceful dolphins (1 min, starting at 10s)
		{ id: 'z8XyD-4lU_c', duration: 60, start: 30 } // Orcas hunting dolphins (1 min, starting at 30s)
	];

	let currentVideoIndex = 0;
	let player;
	let timerId;

	onMount(() => {
		// Dynamically load the YouTube IFrame Player API script
		if (!window.YT) {
			const tag = document.createElement('script');
			tag.src = 'https://www.youtube.com/iframe_api';
			const firstScriptTag = document.getElementsByTagName('script')[0];
			firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
		}

		// Set global callback for when the API is ready
		window.onYouTubeIframeAPIReady = () => {
			initPlayer();
		};

		// If the API script was already loaded on hot-reload/navigation
		if (window.YT && window.YT.Player) {
			initPlayer();
		}

		return () => {
			clearTimeout(timerId);
		};
	});

	function initPlayer() {
		const currentVideo = playlist[currentVideoIndex];
		player = new YT.Player('bg-player', {
			height: '100%',
			width: '100%',
			videoId: currentVideo.id,
			playerVars: {
				autoplay: 1,
				mute: 1,
				controls: 0,
				showinfo: 0,
				rel: 0,
				modestbranding: 1,
				iv_load_policy: 3,
				playsinline: 1,
				start: currentVideo.start
			},
			events: {
				onReady: onPlayerReady,
				onStateChange: onPlayerStateChange
			}
		});
	}

	function onPlayerReady(event) {
		event.target.mute();
		event.target.playVideo();
		startSwitchTimer();
	}

	function onPlayerStateChange(event) {
		// Fallback: If the video ends prematurely on its own
		if (event.data === YT.PlayerState.ENDED) {
			switchVideo();
		}
	}

	function startSwitchTimer() {
		clearTimeout(timerId);
		const currentVideo = playlist[currentVideoIndex];
		timerId = setTimeout(() => {
			switchVideo();
		}, currentVideo.duration * 1000);
	}

	function switchVideo() {
		currentVideoIndex = (currentVideoIndex + 1) % playlist.length;
		const nextVideo = playlist[currentVideoIndex];
		if (player && player.loadVideoById) {
			player.loadVideoById({
				videoId: nextVideo.id,
				startSeconds: nextVideo.start
			});
			startSwitchTimer();
		}
	}
</script>

<!-- Background video container -->
<div class="video-background-container">
	<div class="video-overlay"></div>
	<!-- The YouTube IFrame API replaces this div with the actual iframe -->
	<div id="bg-player"></div>
</div>

<div class="content-wrapper">
	{@render children()}
</div>
