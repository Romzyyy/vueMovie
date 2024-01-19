<script>
import axios from 'axios'

export default {
    data() {
        return {
            movie: {},
        }
    },
    mounted() {
       axios.get('https://api.themoviedb.org/3/discover/movie?api_key=1faf3d5b91fec6bf481a8927461e1814').then((dataMovie) => {
            this.movie = dataMovie.data.results
        })
    },
}
</script>

<template>
    <ul>
      <li v-for="item in movie">{{ item.title }}</li>
    </ul>
</template>
