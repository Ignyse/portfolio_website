<script>
	const interests = [
		{
			label: 'Composing Music',
			color: 'bg-blue-400',
			desktop: { x: -320, y: -140},
			mobile: { x: -110, y: -180 },
            x: -25,   // -28% of container width
            y: -20    // -22% of container height
		},
		{
			label: 'Swimming',
			color: 'bg-cyan-400',
			desktop: { x: 260, y: -120 },
			mobile: { x: 100, y: -120 },
            x: 26,   // -28% of container width
            y: -18    // -22% of container height
		},
		{
			label: 'Design',
			color: 'bg-pink-400',
			desktop: { x: -360, y: 180 },
			mobile: { x: -100, y: 140 },
            x: 26,   // -28% of container width
            y: -18    // -22% of container height
		},
		{
			label: 'Coding',
			color: 'bg-green-400',
			desktop: { x: 280, y: 200 },
			mobile: { x: 90, y: 180 },
            x: 26,   // -28% of container width
            y: -18    // -22% of container height
		},
		{
			label: 'Photography',
			color: 'bg-yellow-400',
			desktop: { x: 0, y: -260 },
			mobile: { x: 0, y: -260 },
            x: 80,   // -28% of container width
            y: -18    // -22% of container height
		}
	];

	let mobile = false;
    let widthWeb = 200;
    let widthMobile = 100;
    let heightWeb = 50;
    let heightMobile = 40;
    let textMobile = 10;
	if (typeof window !== 'undefined') {
		const check = () => {
			mobile = window.innerWidth < 640;
		};

		check();

		window.addEventListener('resize', check);
	}
</script>

<div class="relative h-screen overflow-hidden flex items-center justify-center bg-gray-50">

	<!-- Center -->
	<div class="z-20 text-center">
		<h1 class="text-4xl sm:text-6xl font-semibold text-gray-800 mb-2">
			Ignacy Sus
		</h1>

		<p class="text-gray-500 text-lg">
			Creative Technologist
		</p>
	</div>

	<!-- Bubbles -->
	{#each interests as item}
		<div
        class="absolute"
        style={`
            left: ${50 + item.x}%;
            top: ${50 + item.y}%;
            transform: translate(-50%, -50%);
        `}
		>
			<div
				class={`floating ${item.color} text-white rounded-full px-4 py-2 text-sm font-medium shadow-lg inline-flex items-center justify-center whitespace-nowrap hover:scale-110 transition-transform`}
                style={`
            font-size: ${mobile ? '0.875rem' : '1.5rem'};
            min-width: ${mobile ? '60px' : '70px'};
        `}
			>
				{item.label}
			</div>
		</div>
	{/each}
</div>

<style>
	.floating {
		animation: float 4s ease-in-out infinite;
	}

	@keyframes float {
		0%, 100% {
			transform: translateY(0px);
		}

		50% {
			transform: translateY(-10px);
		}
	}
</style>