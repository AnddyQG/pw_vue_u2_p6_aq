<template>
    <h1 v-if="!pokemonCorrecto">Porfavooor espere.................</h1>
    <div v-else>
        <h1>Selecciona el pokemon correcto:</h1>
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
            const vectorInicial= await obtenerPokemonsFachada(4);
            this.arreglo= vectorInicial;

            const indice= Math.floor(Math.random()*7);
            this.pokemonCorrecto= this.arreglo[indice];
        },
        reviarRespuesta(dato){
            console.log('Se emitio un evento desde el niño')
            console.log(dato);

            if(dato.ident===this.pokemonCorrecto.id){
                this.mostrar=true;
                this.seleccionCorrecta=true;
                this.arreglo=[this.pokemonCorrecto];
                this.mostrarError=false; // Ocultar mensaje de error si la selección es correcta
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
            mostrarError:false // Nueva propiedad para controlar el mensaje de error
        };
    },
    mounted(){
        this.cargaInicial(4);
    }
};
</script>

<style></style>