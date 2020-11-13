<template>
<div class="flex flex-col">
  <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
    <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
      <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
        <table class="min-w-full divide-y divide-gray-200">
          <thead>
            <tr>
              <th class="px-6 py-3 bg-gray-50 text-left text-xs leading-6 font-medium text-gray-500 uppercase tracking-wider">
                Title <br />
                <div class="inline-block relative w-64">
                 <input @input="searchTitle" type="search" class="block appearance-none w-full bg-white border border-gray-400 hover:border-gray-500 px-4 py-2 pr-8 rounded shadow leading-tight focus:outline-none focus:shadow-outline" placeholder="Search by name...">
                 </div>
              </th>
              <th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
                Date 
              </th>
              <th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
                Rate
              </th>
              <th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
                ID
              </th>
         
            </tr>
          </thead>
          <tbody class="bg-white divide-y divide-gray-200">
     
            <tr v-for="(item, index) in this.movie" :key="index" v-on:click="clickDetail(item)">
            
              <td class="px-6 py-4 whitespace-no-wrap">
                <div class="flex items-center">
                  <div class="flex-shrink-0 h-10 w-10">
                    <img class="h-10 w-10 rounded-full" :src="'http://image.tmdb.org/t/p/w185' + item.poster_path" alt="">
                  </div>
                  <div class="ml-4">
                    <div class="text-sm leading-5 font-medium text-gray-900">
                       {{item.title}}
                    </div>
                   
                  </div>
                </div>
              </td>
              <td class="px-6 py-4 whitespace-no-wrap">
                <div class="text-sm leading-5 text-gray-900"> 
                {{item.release_date}}</div>
                
              </td>
              <td class="px-6 py-4 whitespace-no-wrap">
                <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">
                 {{item.vote_average}}
                </span>
              </td>
              <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-500">
                 {{item.id}}
              </td>
        
            </tr>

            <!-- More rows... -->
          </tbody>
        </table>
      </div>
    </div>
  </div>
</div>
</template>

<script lang='ts'>
interface Iitem {
  id: number,
  name: string
}
export default {
    head: {
        title: 'Table'
    },
    props: ['movie'],
    data() {
      return {
      }
    },
    methods: {
      searchTitle(e:string){
        this.$emit('searchTitle', e)
      },
      clickDetail(item:Iitem){
        this.$emit('clickDetail', item)
      }
    }
}
</script>
