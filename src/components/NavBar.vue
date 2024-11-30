<template>
  <nav class="navbar navbar-expand-lg" :style="{ backgroundColor: currentBackgroundColor }">
    <div class="navbar-container">
      <ul class="navbar-nav">
        <li class="nav-item" v-for="(link, index) in navLinks" :key="index">
          <a 
            class="nav-link" 
            :class="{ 'nav-link-hover': true }" 
            :style="{ color: currentLinkColor }" 
            :href="link.href"
          >
            {{ link.text }}
          </a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'NavBar',
  data() {
    return {
      navLinks: [
        { text: 'Login', href: '/login' },
        { text: 'Profile', href: '/portfolio/profile' },
        { text: 'Showcase', href: '/portfolio/showcase' },
        { text: 'Creative', href: '/portfolio/creative' },
        { text: 'Contact', href: '/portfolio/contact' }
      ]
    };
  },
  computed: {
    currentBackgroundColor() {
      return this.$root.currentTheme === 'light-theme' ? '#3C3D42' : '#E0DDCA';
    },
    currentLinkColor() {
      return this.$root.currentTheme === 'light-theme' ? '#9CCD62' : '#3C3D42';
    }
  }
};
</script>

<style scoped>
/* Flexbox to center the navbar content */
.navbar-container {
  display: flex;
  justify-content: center; /* Horizontally center the links */
  align-items: center; /* Vertically align the links */
  width: 100%; /* Ensure it spans the full width */
}

/* Prevent vertical stacking */
.navbar-nav {
  list-style: none;
  display: flex !important; /* Force horizontal layout */
  flex-direction: row !important; /* Prevent vertical stacking */
  padding: 0;
  margin: 0;
}

/* Navbar styles */
.navbar-nav .nav-link {
  font-size: 1 rem; /* Larger font size */
  margin: 0 5px; /* Equal spacing between links */
  border-radius: 5px; /* Rounded corners */
  padding: 5px 10px; /* Padding for better click area */
  transition: background-color 0.3s, color 0.5s; /* Smooth transition for hover effects */
}

/* Light theme hover effect */
.navbar-nav .nav-link-hover:hover {
  background-color: var(--light-hover-color);
  color: var(--light-text);
}

/* Dark theme hover effect */
.dark-theme .navbar-nav .nav-link-hover:hover {
  background-color: var(--dark-hover-color);
  color: var(--dark-text);
}

:root {
  --light-hover-color: #9ccd62;
  --dark-hover-color: #1E1E1E;
  --dark-text: #F6F8E2;
  --light-text: #3C3D42;
}
</style>
