<template>
    <h1 v-if="!pokemonCorrecto">Porfavooor espere.................</h1>
    <div v-else>
        <h1>Selecciona el pokemon correcto:</h1>
        <h2> Puntuacion : {{ puntuacion }}</h2>
        <h2>Intento : {{ intento }}</h2>
        <PokemonImagen :idPokemon="pokemonCorrecto.id" :mostrarPokemon="mostrar"/>
        <PokemonOpciones :pokemons="arreglo"@seleccionPokemon="reviarRespuesta($event)"/>

        <h2 v-if="seleccionCorrecta">Pokemon correcto seleccionado:  {{pokemonCorrecto.nombre  }}</h2>
        <!-- Mensaje de error cuando la selección es incorrecta -->
        <h2 v-if="mostrarError">Pokemon incorrecto, intenta de nuevo.</h2>
    </div>
</template>

<script>
import PokemonImagen from '../components/PokemonImagen'
import PokemonOpciones from '../components/PokemonOpciones'

import obtenerPokemonsFachada from "../clientes/ClientePokemonAPI.js";

export default {
    components: { 
        PokemonImagen,
        PokemonOpciones,
    },
    methods:{
        async cargaInicial(){
            const vectorInicial= await obtenerPokemonsFachada(7);
            this.arreglo= vectorInicial;

            const indice= Math.floor(Math.random()*7);
            this.pokemonCorrecto= this.arreglo[indice];
        },
        reviarRespuesta(dato){
    console.log('Se emitio un evento desde el niño')
    console.log(dato);

    // Incrementar el contador de intentos en cada selección
    this.intento++;

    if(dato.ident===this.pokemonCorrecto.id){
        this.mostrar=true;
        this.seleccionCorrecta=true;
        this.arreglo=[this.pokemonCorrecto];
        this.mostrarError=false; // Ocultar mensaje de error si la selección es correcta

        // Actualizar la puntuación basada en el número de intentos
        switch(this.intento) {
            case 1:
                this.puntuacion = 10;
                break;
            case 2:
                this.puntuacion = 8;
                break;
            case 3:
                this.puntuacion = 5;
                break;
            case 4:
                this.puntuacion = 3;
                break;
            case 5:
                this.puntuacion = 2;
                break;
            case 6:
                this.puntuacion = 1;
                break;
            default:
                this.puntuacion = 0;
        }
    }else{
        console.log('Errrororororor');
        this.mostrarError=true; // Mostrar mensaje de error si la selección es incorrecta
    }
}
    },
    data () {
        return {
            arreglo: [],
            pokemonCorrecto:null,
            mostrar:false,
            seleccionCorrecta:false,
            mostrarError:false, 
            puntuacion :0,
            intento: 0,
       
       
        };
    },
    mounted(){
        this.cargaInicial(7);
    }
};
</script>

<style></style>