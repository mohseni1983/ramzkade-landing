<script lang="ts">
	import { onMount } from 'svelte';

	let canvas: HTMLCanvasElement;
	let ctx: CanvasRenderingContext2D | null = null;
	let animationId: number;
	let particles: Particle[] = [];
	let mouseX = 0;
	let mouseY = 0;

	class Particle {
		x: number;
		y: number;
		vx: number;
		vy: number;
		radius: number;
		color: string;
		opacity: number;
		life: number;
		maxLife: number;

		constructor(width: number, height: number) {
			this.x = Math.random() * width;
			this.y = Math.random() * height;
			this.vx = (Math.random() - 0.5) * 0.5;
			this.vy = (Math.random() - 0.5) * 0.5;
			this.radius = Math.random() * 2 + 1;
			const colors = [
				'rgba(59, 130, 246, 0.5)', // blue
				'rgba(147, 51, 234, 0.5)', // purple
				'rgba(236, 72, 153, 0.5)', // pink
				'rgba(34, 211, 238, 0.5)', // cyan
			];
			this.color = colors[Math.floor(Math.random() * colors.length)];
			this.opacity = Math.random() * 0.5 + 0.2;
			this.maxLife = Math.random() * 200 + 100;
			this.life = this.maxLife;
		}

		update(width: number, height: number) {
			this.x += this.vx;
			this.y += this.vy;

			// Mouse interaction
			const dx = mouseX - this.x;
			const dy = mouseY - this.y;
			const distance = Math.sqrt(dx * dx + dy * dy);
			if (distance < 150) {
				const force = (150 - distance) / 150;
				this.vx -= (dx / distance) * force * 0.02;
				this.vy -= (dy / distance) * force * 0.02;
			}

			// Boundary wrapping
			if (this.x < 0) this.x = width;
			if (this.x > width) this.x = 0;
			if (this.y < 0) this.y = height;
			if (this.y > height) this.y = 0;

			// Damping
			this.vx *= 0.99;
			this.vy *= 0.99;

			this.life--;
			if (this.life <= 0) {
				this.life = this.maxLife;
				this.x = Math.random() * width;
				this.y = Math.random() * height;
			}
		}

		draw(ctx: CanvasRenderingContext2D) {
			ctx.save();
			ctx.globalAlpha = this.opacity * (this.life / this.maxLife);
			ctx.fillStyle = this.color;
			ctx.beginPath();
			ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
			ctx.fill();
			ctx.restore();
		}
	}

	function initCanvas() {
		if (!canvas || !ctx) return;

		const width = window.innerWidth;
		const height = window.innerHeight;
		canvas.width = width;
		canvas.height = height;

		particles = [];
		for (let i = 0; i < 150; i++) {
			particles.push(new Particle(width, height));
		}
	}

	function animate() {
		if (!ctx || !canvas) return;

		ctx.clearRect(0, 0, canvas.width, canvas.height);

		// Draw connections
		ctx.strokeStyle = 'rgba(59, 130, 246, 0.1)';
		ctx.lineWidth = 1;
		for (let i = 0; i < particles.length; i++) {
			for (let j = i + 1; j < particles.length; j++) {
				const dx = particles[i].x - particles[j].x;
				const dy = particles[i].y - particles[j].y;
				const distance = Math.sqrt(dx * dx + dy * dy);

				if (distance < 120) {
					ctx.globalAlpha = (120 - distance) / 120 * 0.3;
					ctx.beginPath();
					ctx.moveTo(particles[i].x, particles[i].y);
					ctx.lineTo(particles[j].x, particles[j].y);
					ctx.stroke();
				}
			}
		}

		// Update and draw particles
		particles.forEach(particle => {
			particle.update(canvas.width, canvas.height);
			particle.draw(ctx!);
		});

		animationId = requestAnimationFrame(animate);
	}

	function handleMouseMove(e: MouseEvent) {
		mouseX = e.clientX;
		mouseY = e.clientY;
	}

	function handleResize() {
		initCanvas();
	}

	onMount(() => {
		if (!canvas) return;
		
		ctx = canvas.getContext('2d');
		if (!ctx) return;
		
		initCanvas();
		animate();

		window.addEventListener('mousemove', handleMouseMove);
		window.addEventListener('resize', handleResize);

		return () => {
			cancelAnimationFrame(animationId);
			window.removeEventListener('mousemove', handleMouseMove);
			window.removeEventListener('resize', handleResize);
		};
	});
</script>

<canvas
	bind:this={canvas}
	class="fixed inset-0 w-full h-full pointer-events-none"
></canvas>

<!-- Gradient Overlays -->
<div class="fixed inset-0 pointer-events-none">
	<div class="absolute inset-0 bg-gradient-to-br from-blue-900/20 via-purple-900/20 to-pink-900/20"></div>
	<div class="absolute inset-0 bg-gradient-to-t from-gray-950 via-transparent to-transparent"></div>
	<div class="absolute top-0 left-0 w-96 h-96 bg-blue-500/10 rounded-full blur-3xl animate-pulse"></div>
	<div class="absolute bottom-0 right-0 w-96 h-96 bg-purple-500/10 rounded-full blur-3xl animate-pulse" style="animation-delay: 1s;"></div>
	<div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-96 h-96 bg-pink-500/10 rounded-full blur-3xl animate-pulse" style="animation-delay: 2s;"></div>
</div>
