<template>
<h1 v-if="!pokemon">Espere por favor...</h1>
<div v-else>
   <h1>Quien es este Pokemon?</h1>
    <PokemonPicture :pokemonId = pokemon.id :showPokemon="showPokemon"/>
    <PokemonOptions :pokemons="pokemonArr" 
    @selection="checkAnswer($event)"
    />
        <template v-if="showAnswer">
<h2>{{message}}</h2>
<button @click="newGame">Nuevo Juego</button>
        </template>


</div>  
</template>

<script>
import PokemonPicture from '@/components/PokemonPicture.vue';
import PokemonOptions from '@/components/PokemonOptions.vue';
import getPokemonOptions from '@/helpers/getPokemonOptions'

// console.log(getPokemonOptions())


export default {
    components: { PokemonPicture, PokemonOptions }, 
    data() {
        return {
            pokemonArr:[],
            pokemon: '',
            showPokemon : false,
            showAnswer: false,
            message:''
        }
    },

methods:{
   async mixPokemonArray(){
        this.pokemonArr = await getPokemonOptions()
        console.log('pppppppp',this.pokemonArr)
        

//Generar un numero random del 0 al 3
const rdnInt = Math.floor(Math.random()*4)
console.log(rdnInt)
this.pokemon = this.pokemonArr [rdnInt]
 console.log('soy yo',this.pokemon)
    },

    checkAnswer(pokemonId){
         this.showAnswer = true
    if (pokemonId=== this.pokemon.id ){
    this.showPokemon = true 
    this.message = `Correcto, ${this.pokemon.name}`  
    
    } else{
        this.message = `Era, ${this.pokemon.name}`
    }
    },

    newGame(){
    window.location.reload();
    }

},

mounted(){
    this.mixPokemonArray()
    console.log( 'soy pokemon arr',this.pokemonArr)
}
}
</script>
