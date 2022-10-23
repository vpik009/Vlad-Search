<template>
  <q-page class="flex flex-center">

    <div full-width q-ml-lg v-if="!result">
      <q-input style="width:100%;" bottom-slots v-model="searchText" label="Search..." dense v-on:keyup.enter="console(searchText)">
        <template v-slot:append>
          <q-icon v-if="searchText !== ''" name="close" @click="clear" class="cursor-pointer" />
          <q-icon name="search" @click="console(searchText)"/>
        </template>
      </q-input>
    </div>


  </q-page>
</template>

<script>
import axios from 'axios'

export default {
    name: 'App',
    data: function() {
        return {
          searchText: "",
          result: null
        }
    },

    methods: {
        console(input) {
          if(input.length){
            console.log(input)
            this.search(input)
          }
        },
        async search(input){
          if(input.length){

            const options = {
              method: 'GET',
              url: 'https://bing-web-search1.p.rapidapi.com/search',
              params: {
                q: input,
                mkt: 'en-us',
                count: 50,
                safeSearch: 'Off',
                textFormat: 'Raw',
                freshness: 'Month'
              },
              headers: {
                'X-BingApis-SDK': 'true',
                'X-RapidAPI-Key': '7a7b15df43mshb4cea7ab16cc7f7p1931a7jsn1eb9bbc7d80c',
                'X-RapidAPI-Host': 'bing-web-search1.p.rapidapi.com'
              }
            };

            axios.request(options).then(function (response) {
              console.log(response.data);
            }).catch(function (error) {
              console.error(error);
            });

          }
        },
        clear(){
          this.searchText='';
        }
    }
}
</script>
