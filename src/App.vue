<script>
import axios from 'axios'
const key = import.meta.env.VUE_APP_API_KEY
const token = import.meta.env.VUE_APP_API_TOKEN
export default {
    name: 'search',
    data() {
        return {
            movie: {},
            query: '',
            results: '',
        }
    },
    mounted() {
        // Definisikan URL dan opsi
        const url =
            'https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=en-US&page=1&sort_by=popularity.desc'
        const options = {
            headers: {
                accept: 'application/json',
                Authorization: token,
            },
        }

        // Gunakan Axios untuk melakukan permintaan HTTP
        axios
            .get(url, options)
            .then((response) => {this.movie = response.data.results})
            .catch((error) => {
                console.error(error)
            })
    },
    methods: {
        searchMovie(query) {
            const options = {
                method: 'GET',
                headers: {
                    accept: 'application/json',
                    Authorization: token,
                },
            }

            fetch(
                `https://api.themoviedb.org/3/search/movie?query=${query}&include_adult=false&language=en-US&page=1`,
                options
            )
                .then((response) => response.json())
                .then((response) => (this.results = response.results))
                .catch((err) => console.error(err))
        },
    },
}
</script>

<template>
    <div class="w-full h-screen">
        <div>
            <form
                @submit.prevent="searchMovie(query)"
                class="w-full flex justify-center items-center lg:mt-20 mt-8">
                <input
                    type="text"
                    v-model="query"
                    placeholder="search movie"
                    class="m-4 p-4 lg:w-1/3 rounded-full outline-none bg-gray-800 text-white w-56" />
                <input
                    type="submit"
                    value="search"
                    class="bg-gray-900 text-white lg:w-28 w-24 rounded-full h-12 cursor-pointer" />
            </form>
        </div>

        <div
            v-if="results.length > 0"
            class="grid lg:grid-cols-4 md:grid-cols-3 grid-cols-2 gap-2 justify-items-center mx-auto px-4 lg:px-60">
            <div
                class="w-full lg:h-[32rem] h-[28rem] lg:mt-20 mt-8 px-4"
                v-for="list in results">
                <img
                    :src="`http://image.tmdb.org/t/p/w500/${list.poster_path}`"
                    :alt="list.title"
                    class="w-full lg:h-[30rem] h-[16rem]" />
                <h1 class="mt-4 font-medium text-lg text-black">
                    {{ list.title }}
                </h1>
                <h1 class="text-lg text-black">
                    Rating {{ list.vote_average }}
                </h1>
            </div>
        </div>

        <div
            v-else
            class="grid lg:grid-cols-4 md:grid-cols-3 grid-cols-2 gap-2 justify-items-center mx-auto px-4 lg:px-60">
            <div
                class="w-full lg:h-[32rem] h-[28rem] lg:mt-20 mt-8 px-4"
                v-for="item in movie">
                <img
                    :src="`http://image.tmdb.org/t/p/w500/${item.poster_path}`"
                    :alt="item.title"
                    class="w-full lg:h-[30rem] h-[16rem]" />
                <h1 class="mt-4 font-medium text-lg text-black">
                    {{ item.title }}
                </h1>
                <h1 class="text-lg text-black">
                    Rating {{ item.vote_average }}
                </h1>
            </div>
        </div>
    </div>
</template>
