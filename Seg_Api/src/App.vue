<script setup>

import PostsUser from './components/PostsUser.vue';
import User from './components/User.vue';
</script>

<template >
        <div>
        <div class=" h-16 bg-blue-500 ">
                <h1 class="pt-3 text-2xl font-bold mb-2 text-white text-center">Publicaciones de los usuario</h1>
        </div>
                <div class="flex">
                        <div class="w-1/3 h-screen overflow-y-auto bg-DDF2FD">
                                <User @userSelected="mostrarPublicaciones" />
                        </div>

                        <div class="w-2/3 h-screen overflow-y-auto bg-DDF2FD rounded overflow-hidden shadow-xl">
                                <PostsUser :id="userIdSeleccionado" />
                        </div>
                </div>
        </div>
</template>
<script>
import PostsUser from './components/PostsUser.vue';
import User from './components/User.vue';

export default {
        components: {
                PostsUser,
                User,
        },
        data() {
                return {
                        userIdSeleccionado: null,
                };
        },
        methods: {
                mostrarPublicaciones(userId) {
                        this.userIdSeleccionado = userId;
                },
        },
};
</script>