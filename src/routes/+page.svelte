<script>
	const dolphinFacts = [
		'Dolphins are known for their playful behavior and intelligence. They have been observed using sea sponges to protect their snouts while foraging on the seafloor.',
		'Each dolphin has a unique signature whistle, which acts just like a human name, allowing individual dolphins to call and identify one another.',
		'Dolphins sleep with only one half of their brain at a time, keeping one eye open to watch for predators and regularly surface for air.',
		'Spinner dolphins (like the ones in our background) are famous for their acrobatic spins. They can leap up to 3 meters (10 feet) out of the water and spin up to 7 times in a single jump!',
		'Dolphins are highly empathetic and social creatures that live in pods. They have been documented helper-sharing and caring for sick or injured members of their group.'
	];

	// Svelte 5 Runes for state management
	let factIndex = $state(0);
	let nameInput = $state('');
	let messageInput = $state('');
	let submittedMessages = $state([
		{
			name: 'Kaito',
			text: 'Stunning background! The dolphins look absolutely magical.',
			date: 'Just now'
		}
	]);
	let showSuccessToast = $state(false);

	function nextFact() {
		factIndex = (factIndex + 1) % dolphinFacts.length;
	}

	function handleSendMessage(e) {
		e.preventDefault();
		if (!nameInput || !messageInput) return;

		submittedMessages = [
			{ name: nameInput, text: messageInput, date: 'Just now' },
			...submittedMessages
		];
		nameInput = '';
		messageInput = '';
		showSuccessToast = true;

		setTimeout(() => {
			showSuccessToast = false;
		}, 4000);
	}
</script>

<svelte:head>
	<title>AquaProfile | Dolphin Explorer Template</title>
	<meta
		name="description"
		content="A beautiful profile template with a live dolphin swimming background."
	/>
</svelte:head>

<!-- Top Navigation Bar -->
<header
	class="w-full py-4 px-6 lg:px-16 flex justify-between items-center glass-panel border-t-0 border-x-0 rounded-none mb-8 sticky top-0 z-50"
>
	<div class="flex items-center gap-3">
		<!-- Dynamic Spinning Wave/Dolphin Icon -->
		<div
			class="w-10 h-10 rounded-full bg-cyan-500/20 flex items-center justify-center border border-cyan-400/30"
		>
			<svg
				class="w-6 h-6 text-cyan-400 floating-anim"
				fill="none"
				stroke="currentColor"
				viewBox="0 0 24 24"
				xmlns="http://www.w3.org/2000/svg"
			>
				<path
					stroke-linecap="round"
					stroke-linejoin="round"
					stroke-width="2"
					d="M13 10V3L4 14h7v7l9-11h-7z"
				></path>
			</svg>
		</div>
		<span
			class="text-xl font-extrabold tracking-wider bg-gradient-to-r from-cyan-400 to-blue-400 bg-clip-text text-transparent"
			>AQUAPROFILE</span
		>
	</div>
	<nav class="flex items-center gap-6">
		<a href="#about" class="text-sm font-medium hover:text-cyan-400 transition-colors">About</a>
		<a href="#skills" class="text-sm font-medium hover:text-cyan-400 transition-colors">Skills</a>
		<a href="#interact" class="text-sm font-medium hover:text-cyan-400 transition-colors"
			>Interactive</a
		>
		<a
			href="#contact"
			class="text-sm font-medium px-4 py-2 rounded-full border border-cyan-400/40 hover:bg-cyan-400/10 hover:border-cyan-400 text-cyan-400 transition-all"
			>Connect</a
		>
	</nav>
</header>

<main
	class="flex-grow max-w-7xl mx-auto w-full px-4 lg:px-8 pb-16 flex flex-col lg:flex-row gap-8 items-start"
>
	<!-- Left Side: Profile Card (Fixed-width on desktop) -->
	<section
		id="about"
		class="w-full lg:w-96 glass-panel p-8 rounded-3xl flex flex-col items-center text-center relative overflow-hidden"
	>
		<!-- Glowing Decorative Circle -->
		<div class="absolute -top-16 -left-16 w-32 h-32 rounded-full bg-cyan-500/10 blur-3xl"></div>

		<!-- Avatar Container with Gradient Border -->
		<div
			class="relative w-40 h-40 rounded-full p-1 bg-gradient-to-tr from-cyan-400 to-blue-600 shadow-xl mb-6 group"
		>
			<div class="w-full h-full rounded-full overflow-hidden bg-slate-900">
				<img
					src="/avatar.png"
					alt="Marina"
					class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105"
				/>
			</div>
			<!-- Online Indicator -->
			<span
				class="absolute bottom-2 right-2 w-5 h-5 rounded-full bg-emerald-500 border-4 border-slate-950 shadow-md flex items-center justify-center"
				title="Active Online"
			></span>
		</div>

		<h1 class="text-3xl font-bold tracking-tight text-white mb-1 glow-text">Marina Blue</h1>
		<p class="text-cyan-400 font-semibold text-sm mb-4 tracking-wider uppercase">
			Full Stack Developer & Ocean Lover
		</p>

		<div
			class="flex items-center gap-2 px-3 py-1.5 rounded-full bg-cyan-500/10 border border-cyan-500/20 text-cyan-300 text-xs font-semibold mb-6"
		>
			<span class="w-2 h-2 rounded-full bg-cyan-400 animate-pulse"></span>
			EXPLORING DEEP OCEAN & WEB APIs
		</div>

		<p class="text-slate-300 text-sm leading-relaxed mb-8">
			Welcome to my space. I combine my passion for marine biology and cutting-edge frontend
			technologies to craft immersive digital experiences. Currently designing beautiful
			applications on Svelte 5.
		</p>

		<!-- Divider -->
		<div class="w-full h-[1px] bg-slate-700/50 mb-6"></div>

		<!-- Social links -->
		<div class="flex gap-4 mb-2">
			<a
				href="https://github.com"
				target="_blank"
				rel="noopener noreferrer"
				class="w-10 h-10 rounded-full bg-slate-800/60 border border-slate-700 flex items-center justify-center hover:bg-cyan-500/20 hover:border-cyan-500 hover:text-cyan-400 transition-all"
			>
				<svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
					<path
						fill-rule="evenodd"
						d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"
						clip-rule="evenodd"
					/>
				</svg>
			</a>
			<a
				href="https://twitter.com"
				target="_blank"
				rel="noopener noreferrer"
				class="w-10 h-10 rounded-full bg-slate-800/60 border border-slate-700 flex items-center justify-center hover:bg-cyan-500/20 hover:border-cyan-500 hover:text-cyan-400 transition-all"
			>
				<svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
					<path
						d="M8.29 20.251c7.547 0 11.675-6.253 11.675-11.675 0-.178 0-.355-.012-.53A8.348 8.348 0 0022 5.92a8.19 8.19 0 01-2.357.646 4.118 4.118 0 001.804-2.27 8.224 8.224 0 01-2.605.996 4.107 4.107 0 00-6.993 3.743 11.65 11.65 0 01-8.457-4.287 4.106 4.106 0 001.27 5.477A4.072 4.072 0 012.8 9.713v.052a4.105 4.105 0 003.292 4.022 4.095 4.095 0 01-1.853.07 4.108 4.108 0 003.834 2.85A8.233 8.233 0 012 18.407a11.616 11.616 0 006.29 1.84"
					/>
				</svg>
			</a>
		</div>
	</section>

	<!-- Right Side: Content Area (Takes remaining space) -->
	<div class="flex-grow w-full flex flex-col gap-8">
		<!-- Section: Skills & Specializations -->
		<section id="skills" class="glass-panel p-8 rounded-3xl w-full">
			<h2 class="text-2xl font-bold tracking-tight text-white mb-6 flex items-center gap-2">
				<svg class="w-6 h-6 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"
					></path>
				</svg>
				Skills & Specialization
			</h2>
			<div class="flex flex-wrap gap-3">
				<span
					class="px-4 py-2 rounded-xl bg-slate-800/50 border border-slate-700 text-sm font-semibold hover:border-cyan-400 transition-colors"
					>Svelte 5 & SvelteKit</span
				>
				<span
					class="px-4 py-2 rounded-xl bg-slate-800/50 border border-slate-700 text-sm font-semibold hover:border-cyan-400 transition-colors"
					>Tailwind CSS v4</span
				>
				<span
					class="px-4 py-2 rounded-xl bg-slate-800/50 border border-slate-700 text-sm font-semibold hover:border-cyan-400 transition-colors"
					>JavaScript (ESNext)</span
				>
				<span
					class="px-4 py-2 rounded-xl bg-slate-800/50 border border-slate-700 text-sm font-semibold hover:border-cyan-400 transition-colors"
					>WebGL / Three.js</span
				>
				<span
					class="px-4 py-2 rounded-xl bg-slate-800/50 border border-slate-700 text-sm font-semibold hover:border-cyan-400 transition-colors"
					>Node.js</span
				>
				<span
					class="px-4 py-2 rounded-xl bg-slate-800/50 border border-slate-700 text-sm font-semibold hover:border-cyan-400 transition-colors"
					>HTML5 Canvas Audio Visualizers</span
				>
				<span
					class="px-4 py-2 rounded-xl bg-slate-800/50 border border-slate-700 text-sm font-semibold hover:border-cyan-400 transition-colors"
					>Marine Bioacoustic Analysis</span
				>
			</div>
		</section>

		<!-- Section: Interactive Facts Generator -->
		<section id="interact" class="glass-panel p-8 rounded-3xl w-full relative overflow-hidden">
			<!-- Glowing decorative background -->
			<div
				class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-64 h-64 rounded-full bg-blue-500/5 blur-3xl pointer-events-none"
			></div>

			<h2 class="text-2xl font-bold tracking-tight text-white mb-4 flex items-center gap-2">
				<svg
					class="w-6 h-6 text-cyan-400 spin-slow-anim"
					fill="none"
					stroke="currentColor"
					viewBox="0 0 24 24"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M19.428 15.428a2 2 0 00-1.022-.547l-2.387-.477a6 6 0 00-3.86.517l-.318.158a6 6 0 01-3.86.517L6.05 15.21a2 2 0 00-1.806.547M8 4h8l-1 1v5.172a2 2 0 00.586 1.414l5 5c1.26 1.26.367 3.414-1.415 3.414H4.828c-1.782 0-2.674-2.154-1.414-3.414l5-5A2 2 0 009 10.172V5L8 4z"
					></path>
				</svg>
				Interactive Ocean Discovery
			</h2>
			<p class="text-slate-400 text-sm mb-6">
				Learn more about the dolphins swimming in our background! Click below to discover
				fascinating marine biology facts.
			</p>

			<!-- Fact Display Area -->
			<div
				class="min-h-32 p-6 rounded-2xl bg-cyan-950/25 border border-cyan-500/20 flex flex-col justify-between mb-6"
			>
				<div class="text-base text-cyan-100 font-medium italic leading-relaxed">
					"{dolphinFacts[factIndex]}"
				</div>
				<div class="text-right text-xs text-cyan-400/80 font-bold tracking-wider mt-4">
					FACT #{factIndex + 1} OF {dolphinFacts.length}
				</div>
			</div>

			<button
				onclick={nextFact}
				class="glow-btn px-6 py-3 rounded-full text-sm font-bold tracking-wider uppercase transition-all duration-300 hover:tracking-widest flex items-center gap-2"
			>
				<span>Next Dolphin Fact</span>
				<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"
					></path>
				</svg>
			</button>
		</section>

		<!-- Section: Guestbook / Message Board -->
		<section
			id="contact"
			class="glass-panel p-8 rounded-3xl w-full flex flex-col md:flex-row gap-8"
		>
			<!-- Left side of container: Message Form -->
			<div class="flex-grow md:w-1/2">
				<h2 class="text-2xl font-bold tracking-tight text-white mb-2 flex items-center gap-2">
					<svg class="w-6 h-6 text-cyan-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M8 10h.01M12 10h.01M16 10h.01M9 16H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-5l-5 5v-5z"
						></path>
					</svg>
					Drop a Message
				</h2>
				<p class="text-slate-400 text-sm mb-6">
					Say hello, share your thoughts about dolphins, or project ideas!
				</p>

				<form onsubmit={handleSendMessage} class="space-y-4">
					<div>
						<label
							for="name"
							class="block text-xs font-bold tracking-wider text-cyan-400 uppercase mb-2"
							>Your Name</label
						>
						<input
							type="text"
							id="name"
							bind:value={nameInput}
							required
							placeholder="Kaito"
							class="w-full bg-slate-900/60 border border-slate-700 focus:border-cyan-400 focus:ring-1 focus:ring-cyan-400 rounded-xl px-4 py-3 text-slate-200 placeholder-slate-600 transition-all outline-none"
						/>
					</div>
					<div>
						<label
							for="message"
							class="block text-xs font-bold tracking-wider text-cyan-400 uppercase mb-2"
							>Message</label
						>
						<textarea
							id="message"
							rows="4"
							bind:value={messageInput}
							required
							placeholder="Amazing website! Let's build something together..."
							class="w-full bg-slate-900/60 border border-slate-700 focus:border-cyan-400 focus:ring-1 focus:ring-cyan-400 rounded-xl px-4 py-3 text-slate-200 placeholder-slate-600 transition-all outline-none resize-none"
						></textarea>
					</div>
					<button
						type="submit"
						class="glow-btn w-full py-3.5 rounded-xl text-sm font-bold tracking-wider uppercase"
					>
						Send Message
					</button>
				</form>
			</div>

			<!-- Right side of container: Message List -->
			<div class="md:w-1/2 flex flex-col">
				<h3 class="text-sm font-bold tracking-wider text-slate-400 uppercase mb-4">
					Live Message Board
				</h3>
				<div class="flex-grow space-y-4 overflow-y-auto max-h-[300px] pr-2">
					{#each submittedMessages as msg}
						<div
							class="p-4 rounded-2xl bg-slate-800/40 border border-slate-700/60 flex flex-col gap-1 transition-all hover:bg-slate-800/60"
						>
							<div class="flex justify-between items-center">
								<span class="text-sm font-bold text-cyan-300">{msg.name}</span>
								<span class="text-[10px] font-medium text-slate-500">{msg.date}</span>
							</div>
							<p class="text-xs text-slate-300 leading-relaxed">{msg.text}</p>
						</div>
					{/each}
				</div>
			</div>
		</section>
	</div>
</main>

<footer
	class="w-full py-8 text-center text-xs text-slate-500 border-t border-slate-800/60 glass-panel bg-transparent rounded-none"
>
	<p>&copy; 2026 AquaProfile. All rights reserved. Ocean background powered by Spinner Dolphins.</p>
</footer>

<!-- Floating Toast Success Message -->
{#if showSuccessToast}
	<div
		class="fixed bottom-6 right-6 z-50 p-4 rounded-2xl bg-cyan-950 border border-cyan-400 text-cyan-200 shadow-2xl flex items-center gap-3 transition-all duration-500 animate-bounce"
	>
		<div class="w-8 h-8 rounded-full bg-cyan-500/20 flex items-center justify-center text-cyan-400">
			<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"
				></path>
			</svg>
		</div>
		<div>
			<h4 class="text-xs font-bold text-white">Message Posted!</h4>
			<p class="text-[10px] text-cyan-300/80">Thank you for visiting AquaProfile.</p>
		</div>
	</div>
{/if}
