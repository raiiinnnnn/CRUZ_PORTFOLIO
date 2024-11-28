<template>
  <div :class="['typing-container', currentTheme]">
    <h1>Type To See Magic!</h1>
    <textarea
      v-model="text"
      @keydown="handleKeydown"
      placeholder="Start typing..."
      rows="10"
      class="form-control"
    ></textarea>
    <!-- Dynamically generate logo bursts -->
    <img
      class="logo-burst"
      v-for="(burst, index) in bursts"
      :key="index"
      :src="burst.image"
      :style="{ left: burst.x + 'px', top: burst.y + 'px' }"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: '',
      sounds: [
        new Audio(require('@/assets/Items_rune_arcane.mp3.mp3')),
        new Audio(require('@/assets/Items_rune_bounty.mp3.mp3')),
        new Audio(require('@/assets/Items_rune_dd.mp3.mp3')),
        new Audio(require('@/assets/Items_rune_haste.mp3.mp3')),
        new Audio(require('@/assets/Items_rune_illusion.mp3.mp3')),
        new Audio(require('@/assets/Items_rune_invis.mp3.mp3')),
        new Audio(require('@/assets/Items_rune_regen.mp3.mp3')),
      ],
      runeImages: [
        require('@/assets/Rune_of_Amplify_Damage_model.webp'),
        require('@/assets/Rune_of_Arcane_model.webp'),
        require('@/assets/Rune_of_Bounty_model.webp'),
        require('@/assets/Rune_of_Haste_model.webp'),
        require('@/assets/Rune_of_Illusion_model.webp'),
        require('@/assets/Rune_of_Invisibility_model.webp'),
        require('@/assets/Rune_of_Regeneration_model.webp'),
        require('@/assets/Rune_of_Shield_model.webp'),
        require('@/assets/Rune_of_Water_model.webp'),
        require('@/assets/Rune_of_Wisdom_model.webp'),
      ],
      bursts: [], // Store positions and images for the logo bursts
    };
  },
  computed: {
    currentTheme() {
      return this.$root.currentTheme; // Access the current theme from the root instance
    },
  },
  methods: {
    handleKeydown(event) {
      this.playSound(event);
      this.burstRunes(event);
    },
    playSound(event) {
      // Play sound only for letter keys (A-Z and a-z)
      if ((event.key >= 'A' && event.key <= 'Z') || (event.key >= 'a' && event.key <= 'z')) {
        const soundIndex = Math.floor(Math.random() * this.sounds.length);
        const soundToPlay = this.sounds[soundIndex];

        soundToPlay.currentTime = 0; // Reset sound to start
        soundToPlay.play().catch((error) => console.error("Error playing sound:", error)); // Play the selected sound
      }
    },
    burstRunes(event) {
      const rect = event.target.getBoundingClientRect();
      const burstCount = 5; // Number of bursts for each keypress

      for (let i = 0; i < burstCount; i++) {
        const x = Math.random() * (rect.width - 50); // Adjust for logo size
        const y = Math.random() * (rect.height - 50); // Adjust for logo size
        const image = this.runeImages[Math.floor(Math.random() * this.runeImages.length)];

        this.bursts.push({ x, y, image });

        // Remove burst after animation
        setTimeout(() => {
          this.bursts.shift();
        }, 1000); // Duration of burst effect
      }
    },
  },
};
</script>

<style scoped>
.typing-container {
  text-align: center;
  margin-top: 50px;
  position: relative;
  max-width: 600px; /* Increase width for better aesthetics */
  margin-left: auto;
  margin-right: auto;
  padding: 20px; /* Add padding for spacing */
  border: 2px solid #9CCD62; /* Border color matching your theme */
  border-radius: 10px; /* Rounded corners */
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2); /* Shadow for depth */
}

.light-theme {
  background-color: #F6F8E2; /* Light background color */
  color: #3C3D42; /* Light text color */
}

.dark-theme {
  background-color: #3C3D42; /* Dark background color */
  color: #F6F8E2; /* Dark text color */
}

textarea {
  padding: 15px; /* More padding for comfort */
  font-size: 18px; /* Increase font size for better readability */
  width: 100%; /* Full width */
  height: 200px;
  resize: none;
  position: relative;
  z-index: 1; /* Ensure textarea is above bursts */
  border-radius: 5px; /* Rounded corners for textarea */
  border: 1px solid #ccc; /* Light border */
  outline: none; /* Remove default outline */
}

textarea:focus {
  border-color: #9CCD62; /* Focus border color */
}

/* Updated: Logo burst styling */
.logo-burst {
  position: absolute;
  width: 50px; /* Adjust to match logo size */
  height: 50px; /* Maintain aspect ratio */
  opacity: 0.8;
  animation: burst 1s ease-out forwards;
}

@keyframes burst {
  from {
    transform: translateY(0);
    opacity: 1;
  }
  to {
    transform: translateY(-50px) scale(1.5); /* Adjust scaling and movement */
    opacity: 0; /* Fade out */
  }
}
</style>
