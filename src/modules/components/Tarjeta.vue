<template>
    <table>
        <tr>
            <img class="mostrar-pokemon" v-if="muestraPockemon" :src="imagenFuente" alt="no se carga la imagen" />

        </tr>

        <tr>
            <td>{{ this.nombrePokemon }}</td>
        </tr>
    </table>
</template>

<script>
export default {

    data() {
        return {
            rutaCuadroNegro: require('./store/imagen2.png'),
            urlDatosPokemon: 'https://pokeapi.co/api/v2/pokemon/id',
            nombreCuadroNegro: 'xxxxxxx',
            nombrePokemon: ''
        }
    },

    name: 'tarjetaJuego',

    props: ['idPokemon'],

    props: {
        pockemonId: {
            type: Number,
            required: true,
        },
        muestraPockemon: {
            type: Boolean,
            required: true,
        },
    },




    setup(props) {
        console.log(props.puntaje)

    },

    methods: {
        async obtenerNombrePokemon() {
            if (this.pockemonId && this.pockemonId > 0) {
                var url = this.urlDatosPokemon.replace('id', this.pockemonId);
                const response = await fetch(url);
                const jsonResponse = await response.json();
                this.nombrePokemon = jsonResponse.name;
            } else {
                this.nombrePokemon = this.nombreCuadroNegro;
            }
        }
    },

    computed: {
        imagenFuente() {
            if (this.pockemonId && this.pockemonId > 0) {
                return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pockemonId}.svg`;
            } else {
                return this.rutaCuadroNegro;
            }
        }
    },

    watch: {
        pockemonId() {
            this.obtenerNombrePokemon();
        }
    },

    mounted() {
        this.obtenerNombrePokemon();
    }

}
</script>

<style>
td {
    text-align: center;
}
</style>