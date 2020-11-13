<template>
    <!--
  Tailwind UI components require Tailwind CSS v1.8 and the @tailwindcss/ui plugin.
  Read the documentation to get started: https://tailwindui.com/documentation
-->
<div>
<div v-if="this.loading" class="loading-page">
    <p>Loading...</p>
</div>
<nav v-else class="bg-gray-800">
  <div class="max-w-7xl mx-auto px-2 sm:px-6 lg:px-8">
    <div class="relative flex items-center justify-between h-16">
      <div class="absolute inset-y-0 left-0 flex items-center sm:hidden">
        <!-- Mobile menu button-->
        <button class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-white hover:bg-gray-700 focus:outline-none focus:bg-gray-700 focus:text-white transition duration-150 ease-in-out" aria-label="Main menu" aria-expanded="false">
          <!-- Icon when menu is closed. -->
          <!--
            Heroicon name: menu

            Menu open: "hidden", Menu closed: "block"
          -->
        
          <svg class="block h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
          </svg>

          <!-- Icon when menu is open. -->
          <!--
            Heroicon name: x

            Menu open: "block", Menu closed: "hidden"
          -->
          <svg class="hidden h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
      <div class="flex-1 flex items-center justify-center sm:items-stretch sm:justify-start">
        <div class="flex-shrink-0">
          <nuxt-link to="/dashboard">
          <img class="block lg:hidden h-8 w-auto" src="https://tailwindui.com/img/logos/v1/workflow-mark-on-dark.svg" alt="Workflow logo">
          <img class="hidden lg:block h-8 w-auto" src="https://tailwindui.com/img/logos/v1/workflow-logo-on-dark.svg" alt="Workflow logo">
         </nuxt-link>
        </div>
        <div class="hidden sm:block sm:ml-6">
          <div class="flex">
            <a href="#" class="px-3 py-2 rounded-md text-sm font-medium leading-5 text-white bg-gray-900 focus:outline-none focus:text-white focus:bg-gray-700 transition duration-150 ease-in-out">
            welcome {{this.name}}
            </a>
          </div>
        </div>

        <filter-genre
          :selectedGenre="this.selectedGenre"
          :genre="this.genre"
          @clickGenre="this.clickGenre"
          @resetGenre="this.resetGenre"
        />
      
      </div>

      <div class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0">
        <button class="p-1 border-2 border-transparent text-gray-400 rounded-full hover:text-white focus:outline-none focus:text-white focus:bg-gray-700 transition duration-150 ease-in-out" aria-label="Notifications" v-on:click="clickLogout">
          <!-- Logout -->
          <svg class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
         </svg>
        </button>

        <!-- Profile dropdown -->
        <div class="ml-3 relative">
          <div>
            <button class="flex text-sm border-2 border-transparent rounded-full focus:outline-none focus:border-white transition duration-150 ease-in-out" id="user-menu" aria-label="User menu" aria-haspopup="true">
              <img class="h-8 w-8 rounded-full" src="https://avatars1.githubusercontent.com/u/11289176?s=460&u=742d904835c5ff776446a7390ce1653fd5f4c89b&v=4" alt="">
            </button>
          </div>
          <!--
            Profile dropdown panel, show/hide based on dropdown state.

            Entering: "transition ease-out duration-100"
              From: "transform opacity-0 scale-95"
              To: "transform opacity-100 scale-100"
            Leaving: "transition ease-in duration-75"
              From: "transform opacity-100 scale-100"
              To: "transform opacity-0 scale-95"
          -->
        
        </div>
      </div>
    </div>
  </div>

  <!--
    Mobile menu, toggle classes based on menu state.

    Menu open: "block", Menu closed: "hidden"
  -->
  <div class="hidden sm:hidden">
    <div class="px-2 pt-2 pb-3">
      <a href="#" class="block px-3 py-2 rounded-md text-base font-medium text-white bg-gray-900 focus:outline-none focus:text-white focus:bg-gray-700 transition duration-150 ease-in-out">Dashboard</a>
      <a href="#" class="mt-1 block px-3 py-2 rounded-md text-base font-medium text-gray-300 hover:text-white hover:bg-gray-700 focus:outline-none focus:text-white focus:bg-gray-700 transition duration-150 ease-in-out">Team</a>
      <a href="#" class="mt-1 block px-3 py-2 rounded-md text-base font-medium text-gray-300 hover:text-white hover:bg-gray-700 focus:outline-none focus:text-white focus:bg-gray-700 transition duration-150 ease-in-out">Projects</a>
      <a href="#" class="mt-1 block px-3 py-2 rounded-md text-base font-medium text-gray-300 hover:text-white hover:bg-gray-700 focus:outline-none focus:text-white focus:bg-gray-700 transition duration-150 ease-in-out">Calendar</a>
    </div>
  </div>
</nav>


<!-- body -->
<table-data
  @searchTitle='this.searchTitle'
  @clickDetail='this.clickDetail'
  :movie='this.movie'
/>


<!-- modal -->
<modal-movie 
  :modal="this.modal" 
  :movieDetail="this.movieDetail"
  @clickDetail="this.clickDetail"
/>

</div>
</template>


<script lang='ts'>

interface Iitem {
  id: number;
  name: string;
  overview?: string;
  poster_path?: string;
}

interface Imovie {
  adult: boolean;
  backdrop_path:string;
  genre_ids: number[];
  id: number
  original_language: string;
  original_title: string;
  overview: string;
  popularity: number;
  poster_path: string;
  release_date: string;
  title: string;
  video: boolean;
  vote_average: number;
  vote_count: number;
  genres: Iitem[];
  filter?: any;
}

interface Igenre {
  genres: Iitem
}

import FilterGenre from '~/components/Filter.vue';
import TableData from '~/components/Table.vue';
import ModalMovie from '~/components/Modal.vue';
import VueRouter, { Route } from 'vue-router'

declare module 'vue/types/vue' {
  interface Vue {
    $router: VueRouter
  }
}

export default {
  
    head: {
        title: 'Dashboard'
    },
    components: {
      FilterGenre,
      TableData,
      ModalMovie
    },
    
    data() {
      return {
        name: <string | null>'',
        loading:<boolean> true,
        modal: <boolean>false,
        movie: <object>[],
        genre: <object>[],
        selectedGenre:<string>'Select Genre',
        movieDetail:<any>{
          title: '',
          genre: '',
          date: '',
          overview: '',
          img: ''
        }
      }
    },
    methods: {
      clickLogout(e:any) {
        e.preventDefault();
        window.sessionStorage.removeItem('email')
        window.sessionStorage.removeItem('statusLogin')
        this.$router.push('/')
      },
      getMovie() {
        fetch(
            'https://api.themoviedb.org/3/movie/top_rated?api_key=bf1b09065cc06d4ff6e4ede4601348ff&language=en-US&page=1'
          ).then(res => res.json())
          .then((res:any) => {
             let listingMovie = res.results
             this.movie = listingMovie
          })  
      },
      searchTitle(e:any) {
        if (e.target.value.length >= 3) {
            fetch(
            `https://api.themoviedb.org/3/search/movie?api_key=bf1b09065cc06d4ff6e4ede4601348ff&language=en-US&query=${e.target.value}&page=1&include_adult=false`
          ).then(res => res.json())
          .then((res:any) => {
             this.movie = res.results
             this.loading = false
             this.selectedGenre = 'Select Genre'
          })  
        } else {
          this.getMovie()
        }
      },
      resetGenre() {
       this.getMovie()
       this.selectedGenre = 'Select Genre'
      },
      getGenre() {
          fetch(
            `https://api.themoviedb.org/3/genre/movie/list?api_key=bf1b09065cc06d4ff6e4ede4601348ff&language=en-US`
          ).then(res => res.json())
          .then((res:any) => {
             this.genre = res.genres
             this.loading = false
          })  
      },
      async clickGenre(item:Iitem) {
         fetch(
            'https://api.themoviedb.org/3/movie/top_rated?api_key=bf1b09065cc06d4ff6e4ede4601348ff&language=en-US&page=1'
          ).then(res => res.json())
          .then((res:any) => {
            let listingMovie:Imovie = res.results
            this.movie = listingMovie.filter((list:Imovie) => {
              return list.genre_ids.includes(item.id) && list
            })
        }) 
        this.selectedGenre = item.name
      },
      clickDetail(item:Iitem) {
        if (this.modal) {
          this.modal = false
          this.movieDetail.title = ''
          this.movieDetail.date = ''
          this.movieDetail.overview = ''
          this.movieDetail.genre = ''
          this.movieDetail.img = ''
        } else {
          this.modal = true
          fetch(
            `https://api.themoviedb.org/3/movie/${item.id}?api_key=bf1b09065cc06d4ff6e4ede4601348ff&language=en-US`
          ).then(res => res.json())
          .then((res:Imovie) => {
            console.log('res', res)
            this.movieDetail.title = res.title
            this.movieDetail.date = res.release_date
            this.movieDetail.overview = item.overview
            this.movieDetail.genre = res.genres.map(a => a.name).join(', ')
            this.movieDetail.img = 'http://image.tmdb.org/t/p/w185' + item.poster_path
          })  
        }
      }
    },
    mounted() {
      this.$nextTick(() => {
        this.$nuxt.$loading.start()
        setTimeout(() => this.$nuxt.$loading.finish(), 500)
      })

      if (window.sessionStorage.getItem('statusLogin') !== 'true') {
          this.$router.push('/')
      } else {
          this.getGenre()
          this.getMovie()
          this.name = window.sessionStorage.getItem('email')
      }
    }
}

</script>

<style>
 .loading-page {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(255, 255, 255, 0.8);
    text-align: center;
    padding-top: 200px;
    font-size: 30px;
    font-family: sans-serif;
  }
  .dropdown:hover .dropdown-menu {
  display: block;
}
.dd-inline{
  display: inline-block;
}
</style>
