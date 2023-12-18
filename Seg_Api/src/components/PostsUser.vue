<template>
    <br />
    <div class="overflow-x-auto flex justify-center items-center">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6 w-full mx-10">
            <div v-for="post in datos" :key="post.id" class="bg-white rounded-lg overflow-hidden shadow-md rounded overflow-hidden shadow-xl">
                <div class="card-image h-48 bg-cover bg-center" :style="{ backgroundImage: `url('/imagen.jpg')` }"></div>
                <div class="card-text p-4">
                    <span class="date text-pink-500">#{{ post.id }} </span>
                    <h3 class="h-14 mt-0.5 text-lg text-gray-900">{{ post.title }}</h3>
                    <p class=" h-24 mt-2 line-clamp-3 text-sm/relaxed text-gray-500">
                        {{ post.body }}
                    </p>
                </div>
                <div class="card-stats grid grid-cols-3 bg-blue-500 hover:bg-blue-700 text-white text-lg font-bold">
                    <div class="stat flex items-center justify-center py-2">
                        <div class="value text-center">
                            <span class="block">5123</span>
                            <span class="block text-sm text-sm-center">Views</span>
                        </div>
                    </div>
                    <div class="stat border-l border-r flex items-center justify-center py-2">
                        <div class="value text-center">
                            <span class="block">32</span>
                            <span class="block text-sm text-sm-center">Comments</span>
                        </div>
                    </div>
                    <div class="stat flex items-center justify-center py-2">
                        <div class="value text-center">
                            <span class="block">4<sup>m</sup></span>
                            <span class="block text-sm text-sm-center">Read</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <br />
</template>

<script>
export default {
    data() {
        return {
            datos: [],
        };
    },
    props: {
        id: String,
    },
    methods: {
        datosTabla(userId) {
            const apiUrl = `https://jsonplaceholder.typicode.com/posts?userId=${userId}`;

            fetch(apiUrl)
                .then((response) => response.json())
                .then((data) => {
                    this.datos = data;
                })
                .catch((error) => {
                    console.error("Error fetching data:", error);
                });
        },
    },
    watch: {
        id(newId) {
            this.datosTabla(newId);
        },
    },
    mounted() {
        if (this.id) {
            this.datosTabla(this.id);
        }
    },
};
</script>
