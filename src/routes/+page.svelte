<script lang="ts">
	import AnimatedBackground from '$lib/components/AnimatedBackground.svelte';
</script>

<AnimatedBackground />

<div class="relative z-10 min-h-screen flex items-center justify-center px-4 py-20 animate-fade-in">
	<div class="max-w-5xl w-full">
		<!-- Main Content -->
		<div class="text-center mb-16">
			<h1 class="text-6xl md:text-8xl font-bold mb-6 bg-gradient-to-r from-blue-400 via-purple-500 to-pink-500 bg-clip-text text-transparent animate-pulse">
				Ramzkade Domains
			</h1>
			<p class="text-2xl md:text-3xl text-gray-300 mb-8 font-light">
				Premium Domain Names Available for Sale
			</p>
		</div>

		<!-- Domain Cards -->
		<div class="grid md:grid-cols-2 gap-8 mb-16">
			<div class="group relative">
				<div class="absolute -inset-0.5 bg-gradient-to-r from-blue-600 to-purple-600 rounded-2xl blur opacity-75 group-hover:opacity-100 transition duration-1000"></div>
				<div class="relative bg-gray-900/90 backdrop-blur-xl rounded-2xl p-8 border border-gray-800">
					<div class="flex items-center justify-between mb-4">
						<h2 class="text-3xl font-bold text-white">ramzkade.com</h2>
						<span class="px-3 py-1 bg-green-500/20 text-green-400 rounded-full text-sm font-semibold">Available</span>
					</div>
					<p class="text-gray-400 mb-6">Premium .com domain - Perfect for your business</p>
					<div class="flex items-center gap-2 text-2xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-purple-500">
						<span>Contact for Price</span>
					</div>
				</div>
			</div>

			<div class="group relative">
				<div class="absolute -inset-0.5 bg-gradient-to-r from-purple-600 to-pink-600 rounded-2xl blur opacity-75 group-hover:opacity-100 transition duration-1000"></div>
				<div class="relative bg-gray-900/90 backdrop-blur-xl rounded-2xl p-8 border border-gray-800">
					<div class="flex items-center justify-between mb-4">
						<h2 class="text-3xl font-bold text-white">ramzkade.ir</h2>
						<span class="px-3 py-1 bg-green-500/20 text-green-400 rounded-full text-sm font-semibold">Available</span>
					</div>
					<p class="text-gray-400 mb-6">Iranian domain extension - Ideal for local market</p>
					<div class="flex items-center gap-2 text-2xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-purple-400 to-pink-500">
						<span>Contact for Price</span>
					</div>
				</div>
			</div>
		</div>

		<!-- Contact Section -->
		<div class="text-center">
			<div class="inline-block group relative">
				<div class="absolute -inset-1 bg-gradient-to-r from-cyan-500 via-blue-500 to-purple-500 rounded-2xl blur opacity-50 group-hover:opacity-75 transition duration-1000"></div>
				<div class="relative bg-gray-900/90 backdrop-blur-xl rounded-2xl p-8 border border-gray-800">
					<h3 class="text-2xl font-bold text-white mb-6">Get in Touch</h3>
					<div class="flex flex-col sm:flex-row gap-4 items-center justify-center">
						<a 
							href="tel:+989105105282" 
							class="px-6 py-3 bg-gradient-to-r from-blue-500 to-purple-600 rounded-lg font-semibold hover:scale-105 transition-transform duration-300 shadow-lg shadow-blue-500/50"
						>
							📞 Call Now
						</a>
						<a 
							href="https://wa.me/989105105282" 
							target="_blank"
							rel="noopener noreferrer"
							class="px-6 py-3 bg-gradient-to-r from-green-500 to-emerald-600 rounded-lg font-semibold hover:scale-105 transition-transform duration-300 shadow-lg shadow-green-500/50"
						>
							💬 WhatsApp
						</a>
					</div>
					<a 
						href="tel:+989105105282" 
						class="text-3xl md:text-4xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 via-blue-500 to-purple-500 hover:scale-110 transition-transform duration-300 inline-block mt-6"
					>
						+98 910 510 5282
					</a>
				</div>
			</div>
		</div>
	</div>
</div>

<style>
	@keyframes fade-in {
		from {
			opacity: 0;
			transform: translateY(20px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	.animate-fade-in {
		animation: fade-in 1s ease-out;
	}
</style>