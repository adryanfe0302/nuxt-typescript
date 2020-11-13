<template>
  <div class="inline-block relative w-64 ml-10">
        <div class="dropdown inline-block relative">
            <button class="bg-gray-300 text-gray-700 font-semibold py-2 px-4 rounded inline-flex items-center">
              <span class="mr-1">{{this.selectedGenre}}</span>
              <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/> </svg>
            </button>
            <ul class="dropdown-menu absolute hidden text-gray-700 pt-1">
            <li v-on:click="getReset()"> 
              <a class="rounded-t bg-gray-200 hover:bg-gray-400 py-2 px-4 block whitespace-no-wrap" href="#">
                <span><svg class="fill-current h-4 dd-inline"  xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M4 2a1 1 0 011 1v2.101a7.002 7.002 0 0111.601 2.566 1 1 0 11-1.885.666A5.002 5.002 0 005.999 7H9a1 1 0 010 2H4a1 1 0 01-1-1V3a1 1 0 011-1zm.008 9.057a1 1 0 011.276.61A5.002 5.002 0 0014.001 13H11a1 1 0 110-2h5a1 1 0 011 1v5a1 1 0 11-2 0v-2.101a7.002 7.002 0 01-11.601-2.566 1 1 0 01.61-1.276z" clip-rule="evenodd" />
              </svg> Reset
              </span>
         
              </a>
            </li>
            <li v-for="(item, index) in this.genre" :key="index" v-on:click="getGenre(item)">
              <a class="rounded-t bg-gray-200 hover:bg-gray-400 py-2 px-4 block whitespace-no-wrap" href="#">
              {{item.name}}
              </a>
            </li>
            </ul>
        </div>
      </div>
</template>

<script lang='ts'>
export default {
    head: {
        title: 'Dashboard'
    },
    props: ['genre', 'selectedGenre', 'clickGenre'],
    data() {
      return {
      }
    },
    methods: {
      getGenre(item:object){
        this.$emit('clickGenre', item)
      },
      getReset(){
        this.$emit('resetGenre')
      }
    }
}
</script>
