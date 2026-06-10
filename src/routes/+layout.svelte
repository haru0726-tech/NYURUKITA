<script>
	import '../app.css';
	let { children } = $props();
</script>

<!-- Fixed full-screen video background of dolphins swimming -->
<div class="video-background-container">
	<div class="video-overlay"></div>
	<iframe
		src="https://www.youtube.com/embed/BpXlJnRw3OY?autoplay=1&mute=1&loop=1&playlist=BpXlJnRw3OY,z8XyD-4lU_c&controls=0&showinfo=0&rel=0&modestbranding=1&iv_load_policy=3&playsinline=1&enablejsapi=1"
		title="Dolphins Swimming Background"
		frameborder="0"
		allow="autoplay; encrypted-media; gyroscope; picture-in-picture"
		allowfullscreen
	></iframe>
</div>

<div class="content-wrapper">
	{@render children()}
</div>
