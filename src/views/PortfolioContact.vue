<template>
  <div class="message-form" :class="currentTheme">
    <h2 class="form-title">Drop a Message</h2>
    <form @submit.prevent="submitMessage">
      <label for="user" class="form-label">User</label>
      <input type="text" id="user" v-model="user" class="form-input" required />

      <label for="message" class="form-label">Message</label>
      <textarea id="message" v-model="message" class="form-textarea" required></textarea>
    </form>

    <!-- Container for Email Me button to be centered -->
    <div class="email-me-container">
      <a :href="generateEmailLink" target="_blank" class="contact-button email-me-button">Email Me</a>
    </div>

    <!-- Contact Buttons with Image Logos (Facebook & Instagram) -->
    <div class="contact-buttons">
      <!-- Facebook Logo -->
      <a :href="facebookUrl" target="_blank" class="contact-button">
        <img src="@/assets/fb.png" alt="Facebook" class="social-logo" />
      </a>

      <!-- Instagram Logo -->
      <a :href="instagramUrl" target="_blank" class="contact-button">
        <img src="@/assets/ig.png" alt="Instagram" class="social-logo" />
      </a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: '',  // User's name or identifier
      message: '', // User's message
      email: '2405.rainielcruz@gmail.com', // Replace with your email
      facebookUrl: 'https://www.facebook.com/raiinathaniiel/', // Replace with your Facebook URL
      instagramUrl: 'https://www.instagram.com/___.nthn/', // Instagram URL
    };
  },
  computed: {
    // Access the current theme from the root instance (light or dark theme)
    currentTheme() {
      return this.$root.currentTheme;
    },
    // Generate the Gmail compose link dynamically based on the User and Message input
    generateEmailLink() {
      let subject = 'Message from ' + this.user;
      let body = '';
      
      // Add user content with "From:" label if it's not empty
      if (this.user) {
        body += `From: ${this.user}\n\n`;
      }
      
      // Add message content if it's not empty
      if (this.message) {
        body += `${this.message}`;
      }

      // Return the URL with encoded subject and body
      return `https://mail.google.com/mail/?view=cm&fs=1&to=${this.email}&su=${encodeURIComponent(subject)}&body=${encodeURIComponent(body)}`;
    }
  },
  methods: {
    // Remove submitMessage method since the Submit button is no longer required
  },
};
</script>

<style scoped>
:root {
  --light-background: #F6F8E2;
  --dark-background: #3C3D42;
  --light-text-color: #3C3D42;
  --dark-text-color: #F6F8E2;
  --accent-color: #9CCD62;
  --highlight-color: #E0DDCA;
  --highlight-text: #3C3D42;
  --contrast-text: #2A2A2A;
  --secondary-accent-color: #FF6347;
}

.light-theme {
  background-color: var(--light-background);
  color: var(--light-text-color);
}

.dark-theme {
  background-color: var(--dark-background);
  color: var(--dark-text-color);
}

.message-form {
  max-width: 600px;
  margin: 40px auto; /* Increased margin to create space from NavBar */
  padding: 30px;
  border: #3C3D42;
  border-radius: 15px;
  box-shadow: 0 6px 30px rgba(0, 0, 0, 0.2);
  transition: background-color 0.5s ease, color 0.5s ease;
  border: 2px solid var(--highlight-color); /* Border for the form */
}

.form-title {
  font-size: 2.5rem;
  font-weight: 800;
  margin-bottom: 35px;
  color: var(--accent-color);
  text-align: center;
  text-transform: uppercase;
}

.form-label {
  font-size: 1.3rem;
  font-weight: 600;
  display: block;
  border: #9CCD62;
  margin-bottom: 5px;
}

.form-input,
.form-textarea {
  width: 100%;
  padding: 12px;
  margin-bottom: 20px;
  border: 0.5px solid #9CCD62; /* Border color using #9CCD62 */
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: 400;
  color: var(--contrast-text);
  background-color: transparent; /* Make background transparent for themes */
  transition: border-color 0.3s ease, box-shadow 0.3s ease; /* Added transition for box-shadow */
}

.form-input:focus,
.form-textarea:focus {
  outline: none;
  border-color: var(--accent-color);
  box-shadow: 0 0 5px var(--accent-color); /* Glow effect on focus */
}

/* Centering the Email Me button */
.email-me-container {
  display: flex;
  justify-content: center; /* Horizontally center the button */
  margin-top: 20px;
}

.contact-buttons {
  display: flex;
  justify-content: center; /* Center the buttons horizontally */
  margin-top: 20px;
}

.contact-button {
  text-decoration: none;
  color: var(--highlight-text);
  padding: 10px 15px;
  border: 2px solid var(--highlight-color);
  border-radius: 6px;
  transition: background-color 0.3s ease, color 0.3s ease, transform 0.3s ease;
  font-weight: 600;
  text-align: center; /* Center the text */
  margin: 0 10px; /* Add margin between buttons */
}

.contact-button:hover {
  background-color: #3C3D42;
  color: #9CCD62;
  transform: translateY(-2px); /* Slightly move up on hover */
}

/* Styling for social media logos */
.social-logo {
  width: 40px; /* Set a fixed size for the logo */
  height: auto;
  display: block;
  margin: 0 auto; /* Center the image inside the button */
}

/* Styling specifically for the Email Me button */
.email-me-button {
  border: 2px solid black; /* Black border for the Email Me button */
  font-size: 1.1rem;
  font-weight: 600;
  padding: 12px 20px; /* Adjusted padding */
  margin-top: 15px;
  color: var(--accent-color);
  text-align: center;
  display: block;
  background-color: #172b17; /* White background to contrast with the border */
  border-radius: 8px; /* Rounded corners for the button */
}

.email-me-button:hover {
  background-color: var(--accent-color);
  color: #fff;
  transform: translateY(-2px); /* Slightly move up on hover */
}
</style>
