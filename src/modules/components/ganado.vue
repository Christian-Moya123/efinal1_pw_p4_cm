<template>
    <div class="ganotexto">Puntaje: {{this.puntaje}}</div>
<div>
    <h2 class="ganotexto">Felicitaciones has ganado un premio de $10.000,00</h2>
</div>

<div><button v-on:click="reiniciarJuego()">Nuevo juego</button></div>
</template>


<script>

export default {


name: 'ganado',
props: ['puntaje'],


setup(props) {
    console.log("el puntaje es ", props.puntaje)

},

methods: {
    reiniciarJuego() {

    }
}
}
</script>

<style>
.ganotexto {
color: blue;
font-size: 30px;
text-align: center;
}

.centrado {
align-self: center;
}
</style>
