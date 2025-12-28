<script lang="ts">
	import { onMount } from 'svelte';

	interface CryptoLogo {
		name: string;
		symbol: string;
		color: string;
	}

	const cryptos: CryptoLogo[] = [
		{ name: 'Bitcoin', symbol: '₿', color: '#F7931A' },
		{ name: 'Ethereum', symbol: 'Ξ', color: '#627EEA' },
		{ name: 'Binance', symbol: 'BNB', color: '#F3BA2F' },
		{ name: 'Solana', symbol: 'SOL', color: '#9945FF' },
		{ name: 'Cardano', symbol: 'ADA', color: '#0033AD' },
		{ name: 'Polygon', symbol: 'MATIC', color: '#8247E5' },
		{ name: 'Chainlink', symbol: 'LINK', color: '#375BD2' },
		{ name: 'Avalanche', symbol: 'AVAX', color: '#E84142' },
		{ name: 'Polkadot', symbol: 'DOT', color: '#E6007A' },
		{ name: 'Litecoin', symbol: 'Ł', color: '#345D9D' },
		{ name: 'Dogecoin', symbol: 'Ð', color: '#C2A633' },
		{ name: 'Ripple', symbol: 'XRP', color: '#23292F' }
	];

	let mounted = false;

	onMount(() => {
		mounted = true;
	});
</script>

<div class="relative w-full h-80 overflow-hidden py-8">
	<div class="absolute inset-0 flex items-center justify-center">
		{#if mounted}
			{#each Array(24) as _, i}
				{@const crypto = cryptos[i % cryptos.length]}
				{@const delay = i * 0.15}
				{@const duration = 4 + (i % 4) * 0.5}
				{@const angle = (i / 24) * Math.PI * 2}
				{@const radius = 120 + (i % 3) * 40}
				{@const x = Math.cos(angle) * radius}
				{@const y = Math.sin(angle) * radius}
				<div
					class="absolute"
					style="
						left: calc(50% + {x}px);
						top: calc(50% + {y}px);
						animation: floatRotate {duration}s ease-in-out infinite;
						animation-delay: {delay}s;
					"
				>
					<div
						class="w-16 h-16 rounded-full flex items-center justify-center transition-all duration-500 hover:scale-150 hover:z-50 cursor-pointer group"
						style="background: linear-gradient(135deg, {crypto.color}30, {crypto.color}60); border: 2px solid {crypto.color}; box-shadow: 0 0 30px {crypto.color}50, inset 0 0 20px {crypto.color}20;"
					>
						<span
							class="text-xl font-bold transition-all duration-300 group-hover:scale-125"
							style="color: {crypto.color}; text-shadow: 0 0 10px {crypto.color};"
						>
							{crypto.symbol}
						</span>
					</div>
				</div>
			{/each}
		{/if}
	</div>
	
	<!-- Additional floating particles -->
	<div class="absolute inset-0">
		{#if mounted}
			{#each Array(15) as _, i}
				{@const delay = i * 0.2}
				{@const duration = 6 + (i % 3)}
				{@const x = (i * 7) % 100}
				<div
					class="absolute w-2 h-2 rounded-full"
					style="
						left: {x}%;
						top: {(i * 11) % 100}%;
						background: rgba(59, 130, 246, 0.4);
						box-shadow: 0 0 10px rgba(59, 130, 246, 0.6);
						animation: sparkle {duration}s ease-in-out infinite;
						animation-delay: {delay}s;
					"
				></div>
			{/each}
		{/if}
	</div>
</div>

<style>
	@keyframes floatRotate {
		0%, 100% {
			transform: translate(0, 0) rotate(0deg) scale(1);
		}
		25% {
			transform: translate(10px, -15px) rotate(90deg) scale(1.1);
		}
		50% {
			transform: translate(-10px, -25px) rotate(180deg) scale(1.2);
		}
		75% {
			transform: translate(15px, -10px) rotate(270deg) scale(1.1);
		}
	}

	@keyframes sparkle {
		0%, 100% {
			opacity: 0.3;
			transform: scale(1);
		}
		50% {
			opacity: 1;
			transform: scale(1.5);
		}
	}
</style>