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
          <input
            v-model="query"
            @keyup.enter="searchMovies"
            type="text"
            placeholder="Search title and add to grid"
          />
        </div>
      </div>
      <hr class="divider" />
    </div>
    <div class="card-grid">
      <div class="movie-card" v-for="movie in movies" :key="movie.id || movie.title">
        <div class="card-image" :style="{ backgroundImage: `url(${getImageUrl(movie)})` }">
          <button class="close-btn" @click="removeMovie(movie)">×</button>
        </div>
        <div class="card-info">
          <h3>{{ movie.title }}</h3>
          <p>{{ movie.overview || movie.desc }}</p>
          <button class="watch-btn">Watch</button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, reactive } from 'vue';
// import batmanImg from '@/assets/images/Batman.jpg';
// import spidermanImg from '@/assets/images/spiderman.jpg';
// import wildwestImg from '@/assets/images/Wild West.jpg';

// Read from .env (Vite exposes variables as VITE_*)
const API_KEY = '73df24bf058b017a74e43bf4ae82e1a5';
const API_URL = import.meta.env.VITE_API_URL || 'https://api.themoviedb.org/3/search/movie';
const POPULAR_URL = import.meta.env.VITE_POPULAR_URL || 'https://api.themoviedb.org/3/movie/popular';
const IMAGE_BASE = import.meta.env.VITE_IMAGE_BASE || 'https://image.tmdb.org/t/p/w500';

const query = ref('');
const movies = ref([]);
const expandedCards = reactive({});


function getShortDescription(movie) {
  const desc = getDescription(movie);
  const words = desc.split(' ');
  if (words.length <= 50) return desc;
  return words.slice(0, 50).join(' ') + '...';
}

function toggleReadMore(movie) {
  expandedCards[movie.id || movie.title] = !expandedCards[movie.id || movie.title];
}

function isLongDescription(movie) {
  return getDescription(movie).split(' ').length > 50;
}

// Fallback movies
// const fallbackMovies = [
//   {
//     title: 'Batman Returns',
//     img: batmanImg,
//     desc: 'A dark knight must protect Gotham from the Penguin and Catwoman.'
//   },
//   {
//     title: 'Wild Wild West',
//     img: wildwestImg,
//     desc: 'Two agents team up to stop a diabolical inventor in the Old West.'
//   },
//   {
//     title: 'The Amazing Spiderman',
//     img: spidermanImg,
//     desc: 'Peter Parker faces new challenges as the web-slinging superhero.'
//   }
// ];

// Get full image URL or fallback to local images for fallback movies
function getImageUrl(movie) {
  if (movie.poster_path) return IMAGE_BASE + movie.poster_path;
  if (movie.img) return movie.img;
  return '';
}

// Fetch 3 popular movies on mount, fallback to local if API fails or returns error
async function fetchInitialMovies() {
  try {
    const res = await fetch(`${POPULAR_URL}?api_key=${API_KEY}&language=en-US&page=1`);
    const data = await res.json();
    if (data.results && data.results.length) {
      movies.value = data.results.slice(0, 3); // Get 3 movies
    } else {
      movies.value = fallbackMovies.slice(0, 3);
    }
  } catch (e) {
    movies.value = fallbackMovies.slice(0, 3);
  }
}

// Search and add movie to grid, fallback to local if API fails
async function searchMovies() {
  if (!query.value.trim()) return;
  try {
    const res = await fetch(`${API_URL}?api_key=${API_KEY}&query=${encodeURIComponent(query.value)}`);
    const data = await res.json();
    if (data.results && data.results.length) {
      data.results.forEach(apiMovie => {
        if (!movies.value.some(m => m.id === apiMovie.id)) {
          movies.value.push(apiMovie);
        }
      });
    } else {
      // Optionally show a message or add a fallback movie
    }
  } catch (e) {
    // Optionally show a message or add a fallback movie
  }
  query.value = '';
}

// Remove movie (works for both API and fallback)
function removeMovie(movie) {
  if (movie.id) {
    movies.value = movies.value.filter(m => m.id !== movie.id);
  } else {
    movies.value = movies.value.filter(m => m.title !== movie.title);
  }
}

onMounted(fetchInitialMovies);
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
  margin-bottom: 30px;
}
.movie-card:hover {
  transform: translateY(-4px) scale(1.02);
}

.card-image {
  position: relative;
  width: 100%;
  height: 530px;
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
  display: flex;
  flex-direction: column;
  flex: 1;
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
  flex: 1;
}

.watch-btn {
  margin-top: 16px;
  background: #ffb300;
  color: #232221;
  border: none;
  border-radius: 3px;
  padding: 10px 28px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s;
  align-self: flex-start;
}
.watch-btn:hover {
  background: #ffd54f;
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