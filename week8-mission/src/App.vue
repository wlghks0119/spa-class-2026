<script setup>
import { ref } from 'vue';
import MovieCard from './components/MovieCard.vue';
import AddMovieForm from './components/AddMovieForm.vue';

const movies = ref([
  { id: 1, title: '인셉션', rating: 9.5, likes: 0, poster: 'https://picsum.photos/seed/inception/300/450' },
  { id: 2, title: '어바웃 타임', rating: 9.2, likes: 0, poster: 'https://picsum.photos/seed/abouttime/300/450' },
  { id: 3, title: '다크 나이트', rating: 9.2, likes: 0, poster: 'https://picsum.photos/seed/darknight/300/450' },
  { id: 4, title: '기생충', rating: 8.9, likes: 0, poster: 'https://picsum.photos/seed/parasite/300/450' }
]);

// 좋아요 로직
const handleLike = (targetId) => {
  const movie = movies.value.find(m => m.id === targetId);
  if (movie) movie.likes++;
};

// 삭제 로직
const handleDelete = (targetId) => {
  movies.value = movies.value.filter(m => m.id !== targetId);
};

// 옵션 B: 영화 추가 로직
const handleAddMovie = (newMovieData) => {
  const newId = movies.value.length ? Math.max(...movies.value.map(m => m.id)) + 1 : 1;
  
  const newMovie = {
    id: newId,
    ...newMovieData,
    likes: 0,
    poster: `https://picsum.photos/seed/${newId}/300/450` // 랜덤 포스터 생성
  };

  movies.value.push(newMovie);
};
</script>

<template>
  <div class="container">
    <h2>🎬 영화 관리 대시보드 (Props & Emit)</h2>
    
    <AddMovieForm @add-movie="handleAddMovie" />

    <main class="movie-grid">
      <MovieCard 
        v-for="m in movies" 
        :key="m.id" 
        :movie="m" 
        @like-movie="handleLike" 
        @delete-movie="handleDelete" 
      />
    </main>
  </div>
</template>

<style scoped>
.container {
  padding: 40px;
  font-family: sans-serif;
  max-width: 900px;
  margin: 0 auto;
  background-color: #f8f9fa;
  min-height: 100vh;
}

h2 {
  text-align: center;
  margin-bottom: 40px;
  color: #34495e;
  font-weight: 800;
}

.movie-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  gap: 25px;
}
</style>