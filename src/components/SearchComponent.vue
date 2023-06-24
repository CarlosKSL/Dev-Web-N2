<template>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="Qual filme você gostaria de locar?" v-model="search" />
      <input type="submit" value="Buscar" />
    </form>
</template>

<script>
    import { ref } from 'vue';
    import env from '@/env.js'


    export default {
        name: 'SearchComponent',
        
        setup () {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    }

    return {
      search,
      movies,
      SearchMovies
    }
  }
    }
</script>
