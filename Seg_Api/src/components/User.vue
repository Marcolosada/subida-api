<template class="">
    <div class="">
        <div v-if="!mostrarContenido" class="">
            <div v-for="user in users" :key="user.id" class=" p-6 ">
                <div class=" bg-white border border-gray-200 rounded-lg shadow-lg p-6  bg-gradient-to-br  from-blue-500  via-blue-400 to-blue-300">
                    <div class="mb-4">
                        <div class="font-bold text-xl mb-2 text-center text-white">{{ user.name }}</div>
                        <p class="text-black-700 text-base">
                            <strong>ID:</strong> {{ user.id }}<br>
                            <strong>Usuario:</strong> {{ user.username }}<br>
                            <strong>Correo:</strong> {{ user.email }}<br>
                            <strong>Teléfono:</strong> {{ user.phone }}<br>
                        </p>
                    </div>
                    <div class="mb-4">
                        <p class="text-black-700 text-base">
                            <div class="text-center"><strong>Domicilio</strong><br></div>
                            <strong>Calle:</strong> {{ user.address.street }}<br>
                            <strong>Suite:</strong> {{ user.address.suite }}<br>
                            <strong>Ciudad:</strong> {{ user.address.city }}<br>
                            <strong>Código Postal:</strong> {{ user.address.zipcode }}<br>
                            <strong>Latitud:</strong> {{ user.address.geo.lat }}<br>
                            <strong>Longitud:</strong> {{ user.address.geo.lng }}
                        </p>
                    </div>
                    <div class="mb-4">
                        <p class="text-black-700 text-base">
                            <strong>Sitio Web:</strong> {{ user.website }}<br>
                            <div class="text-center"><strong>Empresa</strong><br></div>
                            <strong>{{ user.company.name }}</strong><br>
                            <em>{{ user.company.catchPhrase }}</em><br>
                            {{ user.company.bs }}
                        </p>
                    </div>
                    <div class="flex justify-center items-center">
                        <button @click="mostrarPublicaciones(user.id)"
                            class="bg-blue-700 hover:bg-blue-400 text-white items-center font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline-blue active:bg-blue-800">
                            Publicaciones
                        </button>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>

<script>


export default {
    components: {

    },
    data() {
        return {
            users: [], // Aquí almacenaremos los datos de la API
            datos: [],
            idSelect: null,
        };
    },

    methods: {
        datosTabla() {
            fetch("https://jsonplaceholder.typicode.com/users")
                .then((response) => response.json())
                .then((data) => {
                    this.users = data; // Almacenamos los datos de la API en la variable users
                })
                .catch((error) => {
                    console.error("Error fetching data:", error);
                });
        },
        mostrarPublicaciones(userId) {
            this.$emit("userSelected", userId); // Emitir evento con el ID del usuario
        },
    },

    mounted() {
        // En el hook mounted, puedes realizar la petición a la API y obtener los datos
        this.datosTabla()
    },
};
</script>
