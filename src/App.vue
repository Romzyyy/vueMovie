<script>
import axios from 'axios'

export default {
    data() {
        return {
            movie: {},
        }
    },
    mounted() {
        axios
            .get(
                'https://api.themoviedb.org/3/discover/movie?api_key=1faf3d5b91fec6bf481a8927461e1814'
            )
            .then((dataMovie) => {
                console.log((this.movie = dataMovie.data.results))
            })
    },
}
</script>

<template>
    <div class="w-full h-screen">
        <div class="grid place-items-end w-full h-5/6">
            <div
                class="w-full border-r-gray-500 grid justify-items-start pl-24 z-20">
                <div class="flex mt-0 gap-10">
                    <div>
                        <div v-for="(image, index) in movie">
                            <img
                                v-if="index === 0"
                                class="w-[60rem] h-[28rem] object-cover"
                                :src="`http://image.tmdb.org/t/p/w500/${image.poster_path}`"
                                alt="" />
                        </div>
                    </div>
                    <div v-for="(item, index) in movie">
                        <p class="text-2xl mb-10" v-if="index === 0">
                            {{ item.title }}
                        </p>
                        <p class="text-2xl mb-10" v-if="index === 0">
                            {{ item.original_language }}
                        </p>
                        <p class="text-2xl mb-10" v-if="index === 0">
                            {{ item.overview }}
                        </p>
                        <p class="text-2xl mb-10" v-if="index === 0">
                            {{ item.popularity }}
                        </p>
                        <p class="text-2xl mb-10" v-if="index === 0">
                            {{ item.vote_average }}
                        </p>
                    </div>
                </div>
            </div>
            <div
                v-for="(img, index) in movie"
                class="bg-black absolute top-0 w-screen">
                <img
                    v-if="index === 0"
                    :src="`http://image.tmdb.org/t/p/w500/${img.backdrop_path}`"
                    class="h-[49.5rem] w-screen right-0 object-cover"
                    alt="" />
            </div>
            <div
                class="grid grid-cols-3 gap-2 w-[28rem] h-[14rem] mx-4 -mt-60 z-10">
                <div class="w-full h-full" v-for="(img, index) in movie">
                    <img
                        v-if="index < 3"
                        :src="`http://image.tmdb.org/t/p/w500/${img.poster_path}`"
                        alt="" />
                </div>
            </div>
        </div>

        <div class="grid grid-cols-4 gap-2 justify-items-center mx-auto px-60">
            <div class="w-full h-[32rem] mt-20 px-4" v-for="item in movie">
                <img
                    :src="`http://image.tmdb.org/t/p/w500/${item.poster_path}`"
                    :alt="item.title"
                    class="w-full h-[30rem]" />
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
