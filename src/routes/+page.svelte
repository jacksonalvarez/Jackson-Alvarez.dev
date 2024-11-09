<script>
    import emailjs from 'emailjs-com';
    import { onMount } from 'svelte';

    // Initialize EmailJS on mount
    onMount(() => {
        emailjs.init('FSSyM2wdBcC14IGPQ'); // Replace with your actual EmailJS user ID
    });

    // Function to send email
    async function sendEmail(event) {
        event.preventDefault();

        const name = document.getElementById('name').value;
        const email = document.getElementById('email').value;
        const message = document.getElementById('message').value;

        try {
            const response = await emailjs.send('service_gxfowql', 'template_cxovil8', {
                from_name: name,
                from_email: email,
                message: message
            });
            document.getElementById('email-form').reset();
            closeModal();
        } catch (error) {
            alert('Failed to send email. I probably hit the max token limit @-@ ' + error.text);
        }
    }

    // State for modal visibility
    let isModalVisible = false;
    
    // Functions to open and close modal
    function openModal() {
        isModalVisible = true;
    }

    function closeModal() {
        isModalVisible = false;
    }
</script>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center flex flex-col items-center">
		<h2 class="h2">- Jackson Alvarez -</h2>
		
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
My dream is to develop software that makes a difference. I enjoy creating engaging,
            responsive applications and exploring new technologies. Currently looking for full time work.
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
			<a class="btn variant-filled" href="Resume-JacksonAlvarez-Developer.pdf" download>Résumé</a>
            <button class="btn variant-filled" on:click={openModal}>Email me</button>

		</div>


		
	</div>
</div>
<!-- Email Modal -->
{#if isModalVisible}
    <div id="email-modal" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50">
        <div class="bg-white p-6 rounded-lg max-w-md w-full relative space-y-4 animate-wobble-in">
            <h3 class="text-xl font-semibold text-center">Contact Me</h3>
            <form id="email-form" class="space-y-4" on:submit={sendEmail}>
                <div>
                    <label for="name" class="block text-sm font-medium text-gray-700">Your Name</label>
                    <input type="text" id="name" class="w-full border-gray-300 rounded-md text-gray-700" required />
                </div>
                <div>
                    <label for="email" class="block text-sm font-medium text-gray-700">Your Email</label>
                    <input type="email" id="email" class="w-full border-gray-300 rounded-md text-gray-700" required />
                </div>
                <div>
                    <label for="message" class="block text-sm font-medium text-gray-700">Message</label>
                    <textarea id="message" class="w-full border-gray-300 rounded-md text-gray-700" rows="4" required></textarea>
                </div>
                <button type="submit" class="btn variant-filled w-full">Send</button>
            </form>
            <!-- Close Button -->
            <button class="absolute top-4 right-4 text-gray-500 hover:text-gray-700" on:click={closeModal}>
                &times;
            </button>
        </div>
    </div>
{/if}

<!-- Tailwind + Custom CSS for Wobble Animation -->
<style>
    @keyframes wobble-in {
        0% {
            transform: translateX(-50%) rotate(5deg);
        }
        15% {
            transform: translateX(3%) rotate(-3deg);
        }
        30% {
            transform: translateX(-2%) rotate(2deg);
        }
        45% {
            transform: translateX(1%) rotate(-1deg);
        }
        60% {
            transform: translateX(-1%) rotate(0deg);
        }
        100% {
            transform: translateX(0) rotate(0deg);
        }
    }

    .animate-wobble-in {
        animation: wobble-in 1s ease-in-out;
    }

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