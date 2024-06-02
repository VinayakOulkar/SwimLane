<template>
  <div>
    <MoviesList />
  </div>
</template>

<script>

import MoviesList from './components/MoviesList.vue';

export default {
  name: 'App',
  components: {
    MoviesList
  }
}

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans:ital,wght@0,100..900;1,100..900&display=swap');

*{
  font-family: Noto Sans,sans-serif;
}
</style>
