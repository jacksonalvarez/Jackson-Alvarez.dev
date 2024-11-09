<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center flex flex-col items-center">
		<h2 class="h2">Hey I'm Jack</h2>
		
		<!-- Animated Background and Profile Image -->
		<figure class="relative">
			<section class="img-bg"></section>
			<img
				src="C0019T01.jpg" 
				alt="Jackson Alvarez" 
				class="w-48 h-48 md:w-64 md:h-64 rounded-full object-cover shadow-lg relative z-10"
			/>
		</figure>
		
		<p class="text-lg">
A passionate developer with experience in
            system administration and application development. I enjoy creating engaging,
            responsive applications and exploring new technologies.
		</p>

		<!-- Button with Personal Link -->
		<div class="flex justify-center space-x-2">
			<a
				href="https://www.linkedin.com/in/jackson-alvarez-911b12187/"
				target="_blank"
				rel="noreferrer"
			>
				<img
					src="174857.png" 
					alt="LinkedIn"
					class="w-10 h-10 md:w-10 md:h-10" 
				/>
			</a>

			<a
				href="https://github.com/jacksonalvarez"
				target="_blank"
				rel="noreferrer"
			>
				<img
					src="25231.png" 
					alt="GitHub"
					class="w-10 h-10 md:w-10 md:h-10" 
				/>
			</a>
			<a
				class="btn variant-filled"
				href="Technical Resume2024-9_5_24-Jackson Alvarez (3).pdf"
				target="_blank"
				rel="noreferrer"
				download
			>
				Résumé
			</a>
			<a
				class="btn variant-filled"
				href="https://skeleton.dev/"
				target="_blank"
				rel="noreferrer"
			>
				Email me
			</a>

		</div>


		
	</div>
</div>

<style lang="postcss">
/* General figure styles */
figure {
	@apply flex relative flex-col items-center;
}

/* SVG and background styling for logo */
figure svg,
.img-bg {
	@apply w-64 h-64 md:w-80 md:h-80;
}

/* Background animation */
.img-bg {
	@apply absolute z-[-1] rounded-full blur-[50px] transition-all;
	animation: pulse 5s cubic-bezier(0, 0, 0, 0.5) infinite,
		glow 5s linear infinite;
}

/* Keyframes for the glowing and pulsing background */
@keyframes glow {
	0% {
		@apply bg-primary-400/50;
	}
	33% {
		@apply bg-secondary-400/50;
	}
	66% {
		@apply bg-tertiary-400/50;
	}
	100% {
		@apply bg-primary-400/50;
	}
}

@keyframes pulse {
	50% {
		transform: scale(1.5);
	}
}
</style>
