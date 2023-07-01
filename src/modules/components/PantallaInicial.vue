<template>
    <table v-if="!mostrarGano && !mostrarPerdio">
        <tr>
            <td class="subtitulo">Puntaje: {{ puntaje }}</td>
            <td class="subtitulo">Intento: {{ intento }}</td>
        </tr>

        <tr>


            <td>
                <Tarjeta :pockemonId="idAleatori1" :muestraPockemon="true"></Tarjeta>
            </td>
            <td>
                <Tarjeta :pockemonId="idAleatori2" :muestraPockemon="true"></Tarjeta>
            </td>
            <td>
                <Tarjeta :pockemonId="idAleatori3" :muestraPockemon="true"></Tarjeta>
            </td>

        </tr>

        <tr>
            <td colspan="3"><button v-on:click="jugar()">Jugar</button></td>
        </tr>

    </table>

    <ganado v-if=this.mostrarGano></ganado>
    <perdido v-if=this.mostrarPerdio></perdido>
</template>

<script>

import ganado from './ganado.vue'
import perdido from './perdido.vue'
import Tarjeta from './Tarjeta.vue'
export default {

    name: 'PantallInicial',
    data() {
        return {

            puntaje: 0,
            intento: 0,
            mostrarGano: false,
            mostrarPerdio: false,
            idAleatori1: 0,
            idAleatori2: 0,
            idAleatori3: 0,
            listaIdPokemon: [],
            minPuntaje: 10,
            idMaxPokemon: 500


        };
    },

    components: {
        ganado,
        perdido,
        Tarjeta
    },

    methods: {

        jugar() {
            if (this.intento == 0) {
                this.listaIdPokemon = []
                this.listaIdPokemon.push(this.generarIdPokemon(this.listaIdPokemon))
                this.listaIdPokemon.push(this.generarIdPokemon(this.listaIdPokemon))
                this.listaIdPokemon.push(this.generarIdPokemon(this.listaIdPokemon))
                this.listaIdPokemon.push(this.generarIdPokemon(this.listaIdPokemon))
                this.listaIdPokemon.push(this.generarIdPokemon(this.listaIdPokemon))
                this.listaIdPokemon.forEach(element => console.log(element));

            }

            this.idAleatori1 = this.listaIdPokemon[Math.floor(Math.random() * 5)]
            this.idAleatori2 = this.listaIdPokemon[Math.floor(Math.random() * 5)]
            this.idAleatori3 = this.listaIdPokemon[Math.floor(Math.random() * 5)]
            this.puntaje = this.puntaje + this.retornarPuntaje()

            if (this.puntaje >= this.minPuntaje) {
                this.mostrarGano = true

            } else {
                this.logicaGanarPerder()


                console.log(this.intento)
                console.log(this.puntaje)
                console.log("ale1", this.idAleatori1)
                console.log("ale2", this.idAleatori2)
                console.log("ale3", this.idAleatori3)
                this.intento = this.intento + 1

            }


        },



        retornarPuntaje() {


            if (this.idAleatori1 == this.idAleatori2 && this.idAleatori1 == this.idAleatori3) {
                return 5
            } else if ((this.idAleatori1 == this.idAleatori2 || this.idAleatori1 == this.idAleatori3) && this.idAleatori2 != this.idAleatori3) {
                return 2
            } else if ((this.idAleatori2 == this.idAleatori3 || this.idAleatori2 == this.idAleatori1) && this.idAleatori1 != this.idAleatori3) {
                return 2
            } else {
                return 0
            }
        },


        logicaGanarPerder() {

            if (this.intento == 4) {
                if (this.puntaje < this.minPuntaje) {
                    this.mostrarPerdio = true

                } else {
                    this.mostrarGano = true
                }

            }

        },

        generarIdPokemon(existentes) {
            if (existentes && existentes.length > 0) {
                var auxId = -1
                var i = 0
                var existe = false
                do {
                    auxId = Math.floor(Math.random() * this.idMaxPokemon) + 1

                    for (i = 0; i < existentes.length; i++) {
                        if (existentes.at(i) == auxId) {
                            existe = true
                            break
                        }
                    }


                } while (existe);
                return auxId

            }
            return Math.floor(Math.random() * this.idMaxPokemon) + 1


        }




    }


}


</script>

<style>
button {
    width: 200px;
    height: 50px;
    border-color: black;
    border-width: 5px;
    font-size: 25px;
    background-color: white;
}

.subtitulo {
    font-size: 25px;
}

table {
    width: 100%;
}
</style>
