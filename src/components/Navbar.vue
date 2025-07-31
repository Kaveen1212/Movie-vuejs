<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const showNavbar = ref(true);
const showMenu = ref(false);

let lastScrollY = window.scrollY;

function handleScroll() {
  if (window.scrollY > lastScrollY && window.scrollY > 50) {
    showNavbar.value = false;
  } else {
    showNavbar.value = true;
  }
  lastScrollY = window.scrollY;
}

function toggleMenu() {
  showMenu.value = !showMenu.value;
}

function closeMenu() {
  showMenu.value = false;
}

function handleClickOutside(event) {
  if (
    showMenu.value &&
    !event.target.closest('.navbar') &&
    !event.target.closest('.mobile-menu')
  ) {
    closeMenu();
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
  window.addEventListener('click', handleClickOutside);
});
onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
  window.removeEventListener('click', handleClickOutside);
});
</script>

<template>
  <nav class="navbar" :class="{ 'navbar--hidden': !showNavbar }">
    <div class="navbar__logo">
      <svg width="48" height="48" viewBox="0 0 48 48" fill="none">
        <circle cx="24" cy="24" r="10" stroke="#FFC300" stroke-width="4"/>
        <g stroke="#FFC300" stroke-width="4">
          <line x1="24" y1="2" x2="24" y2="12"/>
          <line x1="24" y1="36" x2="24" y2="46"/>
          <line x1="2" y1="24" x2="12" y2="24"/>
          <line x1="36" y1="24" x2="46" y2="24"/>
          <line x1="8.5" y1="8.5" x2="16" y2="16"/>
          <line x1="39.5" y1="8.5" x2="32" y2="16"/>
          <line x1="8.5" y1="39.5" x2="16" y2="32"/>
          <line x1="39.5" y1="39.5" x2="32" y2="32"/>
        </g>
      </svg>
      <span class="navbar__brand">Logoipsum</span>
    </div>
    <ul class="navbar__links">
      <li><a href="#">HOME</a></li>
      <li><a href="#">OUR SCREENS</a></li>
      <li><a href="#">SCHEDULE</a></li>
      <li><a href="#" class="active">MOVIE LIBRARY</a></li>
      <li><a href="#">LOCATION & CONTACT</a></li>
    </ul>
    <div class="navbar__menu" @click.stop="toggleMenu">
      <span></span>
      <span></span>
      <span></span>
    </div>
    <transition name="fade">
      <ul v-if="showMenu" class="mobile-menu">
        <li><a href="#" @click="closeMenu">HOME</a></li>
        <li><a href="#" @click="closeMenu">OUR SCREENS</a></li>
        <li><a href="#" @click="closeMenu">SCHEDULE</a></li>
        <li><a href="#" class="active" @click="closeMenu">MOVIE LIBRARY</a></li>
        <li><a href="#" @click="closeMenu">LOCATION & CONTACT</a></li>
      </ul>
    </transition>
  </nav>
</template>

<style scoped>
.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: transparent;
  border-bottom: #fff;
  padding: 0 100px;
  height: 90px;
  border-bottom: 1px solid #222;
  position: fixed;   
  top: 0;      
  left: 0;   
  width: 100vw;
  z-index: 1000;
  gap: 10px; 
  transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

.navbar--hidden {
  transform: translateY(-100%);
}

.navbar__logo {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  left: 10px;
}

.navbar__brand {
  color: #fff;
  font-weight: bold;
  font-size: 2rem;
  font-family: 'Montserrat', Arial, sans-serif;
}

.navbar__links {
  display: flex;
  gap: 2rem;
  list-style: none;
  margin-left: 450px;
  padding: 0;
}

.navbar__links a {
  color: #fff;
  text-decoration: none;
  font-size: 1.2rem;
  letter-spacing: 0.05em;
  font-family: 'Montserrat', Arial, sans-serif;
  transition: color 0.2s;
}

.navbar__links a.active,
.navbar__links a:hover {
  text-decoration: underline;
  font-weight: bold;
}

.navbar__menu {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 7px;
  cursor: pointer;
}

.navbar__menu span {
  display: block;
  width: 36px;
  height: 4px;
  background: #fff;
  border-radius: 2px;
}


/* Mobile styles */
@media only screen and (max-width:800px) {
  .navbar {
    padding: 0 15px;
    height: 70px;
  }
  .navbar__logo svg {
    width: 38px;
    height: 38px;
  }
  .navbar__brand {
    font-size: 1.2rem;
  }
  .navbar__links {
    display: none;
  }
  
}
/* Mobile menu styles */
.mobile-menu {
  position: fixed;
  top: 70px;
  left: 0;
  width: 100vw;
  background: #191919;
  z-index: 2000;
  display: flex;
  flex-direction: column;
  gap: 0;
  padding: 0;
  margin: 0;
  list-style: none;
  border-top: 1px solid #222;
  box-shadow: 0 4px 24px rgba(0,0,0,0.2);
}
.mobile-menu li {
  border-bottom: 1px solid #222;
}
.mobile-menu a {
  display: block;
  color: #fff;
  padding: 18px 24px;
  font-size: 1.2rem;
  text-decoration: none;
  font-family: 'Montserrat', Arial, sans-serif;
}
.mobile-menu a.active,
.mobile-menu a:hover {
  text-decoration: underline;
  font-weight: bold;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style>