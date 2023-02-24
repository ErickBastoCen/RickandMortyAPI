<script>
import axios from 'axios'
let API_URL = `https://rickandmortyapi.com/api/character`
export default {
  data() {
    return {
      info: [],
      personajes: [],
      cont:2
    }
  },
  mounted() {
    axios.get(API_URL)
      .then((response) => {
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
  },
  methods: {
    pag(num) {
      API_URL='https://rickandmortyapi.com/api/character/?page='+num
      console.log(API_URL)
      axios.get(API_URL)
      .then((response) => {
        console.log(response.config)
        this.info = response.data.info;
        this.personajes = response.data.results;

      })
      this.cont++
    }
  },
}
</script>

<template>
    <h1 class="text-2xl font-bold mt-10 mb-5"> Rick & Morty</h1>
    <h2 class="text-2xl font-bold mt-10 mb-5">Hay {{ info.count }} personajes en el programa</h2>
    
    <br>
    <br>
    <button @click="pag(cont)">página {{ cont-1 }}</button>
    <br>
    <br>

    <ul>
        <li v-for="p in personajes">
    
            <div class="flex flex-col bg-white border shadow-sm rounded-xl p-4 md:p-5 dark:bg-gray-800 dark:border-gray-700 dark:shadow-slate-700/[.7]">
            <h3 class="text-lg font-bold text-gray-800 dark:text-white">
                Nombre: {{ p.name }}
            </h3>
            <p class="mt-1 text-xs font-medium uppercase text-gray-500 dark:text-gray-500">
                Numero: {{ p.id }}
            </p>
            <br>
            <img class="rounded-t-lg" src="https://rickandmortyapi.com/api/character/avatar/2.jpeg">
            <br>
            <p class="mt-2 text-gray-800 dark:text-gray-400">
                Status: {{ p.status }}
            </p>
            <p class="mt-2 text-gray-800 dark:text-gray-400">
                Especie: {{ p.species }}
            </p>
            <p class="mt-2 text-gray-800 dark:text-gray-400">
                Tipo:  {{ p.type }}
            </p>
            <p class="mt-2 text-gray-800 dark:text-gray-400">
                Género: {{ p.gender }}
            </p>
            <p class="mt-2 text-gray-800 dark:text-gray-400">
                Visto por primera vez en: {{ p.origin.name }}
            </p>          
            <p class="mt-2 text-gray-800 dark:text-gray-400">
                Visto por última vez en: {{ p.location.name }}
            </p>   
            </div>
            <br>
        </li>
    </ul>
</template>