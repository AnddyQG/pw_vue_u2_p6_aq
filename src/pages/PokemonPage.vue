<template>
    <h1>Selecciona el pokemon correcto:</h1>
    <PokemonImagen :idPokemon="383" :mostrarPokemon="false"/>
    <PokemonOpciones :pokemons="arreglo" />
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
        },
    },
    data () {
        return {
            arreglo: [],
            
        };

    },
    mounted(){
        this.cargaInicial(5);
    }

};
</script>

<style></style>