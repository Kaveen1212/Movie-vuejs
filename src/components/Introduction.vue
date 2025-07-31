<template>
  <section class="intro-section">
    <div class="intro-header-wrapper">
      <div class="intro-header">
        <h2>Collect your favourites</h2>
        <div class="search-bar">
          <span class="search-icon" aria-label="Search">
            <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
              <circle cx="9" cy="9" r="7" stroke="#ccc" stroke-width="2"/>
              <line x1="14.2" y1="14.2" x2="18" y2="18" stroke="#ccc" stroke-width="2" stroke-linecap="round"/>
            </svg>
          </span>
          <input type="text" placeholder="Search title and add to grid" />
        </div>
      </div>
      <hr class="divider" />
    </div>
    <div class="card-grid">
      <div class="movie-card" v-for="movie in movies" :key="movie.title">
        <div class="card-image" :style="{ backgroundImage: `url(${movie.img})` }">
          <button class="close-btn" @click="removeMovie(movie)">×</button>
        </div>
        <div class="card-info">
          <h3>{{ movie.title }}</h3>
          <p>{{ movie.desc }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';
import batmanImg from '@/assets/images/batman.jpg';
import spidermanImg from '@/assets/images/spiderman.jpg';
import wildwestImg from '@/assets/images/Wild West.jpg';

const movies = ref([
  {
    title: 'Batman Returns',
    img: batmanImg,
    desc: 'Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut...'
  },
  {
    title: 'Wild Wild West',
    img: wildwestImg,
    desc: 'Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut...'
  },
  {
    title: 'The Amazing Spiderman',
    img: spidermanImg,
    desc: 'Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut...'
  }
]);

function removeMovie(movie) {
  movies.value = movies.value.filter(m => m !== movie);
}
</script>

<style scoped>
.intro-section {
  background: #232221;
  padding: 40px 0 0 0;
  min-height: 100vh;
  color: #fff;
  font-family: 'Montserrat', Arial, sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.intro-header-wrapper {
  width: 100%;
  max-width: 1536px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.intro-header {
  width: 100%;
  max-width: 1536px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 24px;
  margin-bottom: 0;
}

.intro-header h2 {
  font-size: 2rem;
  letter-spacing: 0.08em;
  font-weight: 500;
  margin: 0;
  white-space: nowrap;
}

.search-bar {
  display: flex;
  align-items: center;
  border: 1px solid #aaa;
  border-radius: 4px;
  padding: 0 12px;
  background: transparent;
  height: 38px;
  min-width: 320px;
  width: 100%;
  max-width: 350px;
}

.search-icon {
  font-size: 1.2rem;
  margin-right: 8px;
  color: #ccc;
  justify-content: center;
}

.search-bar input {
  background: transparent;
  border: none;
  outline: none;
  color: #fff;
  font-size: 1rem;
  width: 100%;
}

.divider {
  border: none;
  border-top: 2px solid #444;
  margin: 32px 0 24px 0;
  width: 100%;
  max-width: 1536px;
}

.card-grid {
  display: flex;
  gap: 42px;
  flex-wrap: wrap;
  justify-content: center;
  width: 100%;
  max-width: 1536px;
  margin: 0 auto;
}

.movie-card {
  background: #2d2c2b;
  border-radius: 2px;
  overflow: hidden;
  width: 480px;
  display: flex;
  flex-direction: column;
  box-shadow: 0 2px 8px rgba(0,0,0,0.12);
  transition: transform 0.2s;
}
.movie-card:hover {
  transform: translateY(-4px) scale(1.02);
}

.card-image {
  position: relative;
  width: 100%;
  height: 630px;
  background-size: cover;
  background-position: center;
}

.close-btn {
  position: absolute;
  top: 16px;
  right: 16px;
  background: #333;
  color: #fff;
  border: none;
  border-radius: 2px;
  width: 32px;
  height: 32px;
  font-size: 1.3rem;
  cursor: pointer;
  opacity: 0.85;
  transition: background 0.2s;
}
.close-btn:hover {
  background: #444;
}

.card-info {
  padding: 20px 16px 16px 16px;
}

.card-info h3 {
  font-size: 1.3rem;
  font-weight: 600;
  letter-spacing: 0.06em;
  margin: 0 0 12px 0;
}

.card-info p {
  font-size: 1rem;
  color: #ccc;
  margin: 0;
}

/* Responsive styles */
@media (max-width: 1536px) {
  .intro-header-wrapper,
  .intro-header,
  .divider,
  .card-grid {
    max-width: 100%;
  }
}

@media (max-width: 700px) {
  .intro-header {
    flex-direction: column;
    align-items: center;
    gap: 12px;
    max-width: 350px;
  }
  .intro-header-wrapper,
  .divider,
  .card-grid {
    max-width: 350px;
  }
  .card-grid {
    flex-direction: column;
    gap: 20px;
    align-items: center;
  }
  .movie-card {
    width: 100%;
    max-width: 350px;
    margin-bottom: 30px;
  }
  .card-image {
    height: 450px;
  }
}

</style>