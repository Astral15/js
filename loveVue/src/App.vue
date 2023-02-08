<script>

import axios from 'axios'

export default {
    
    data() { 
      return {
        langs: ['Geo', 'Eng'],
        range: [4,5,10,20],
        limit: 10,
        lang: 'ge',
        apiUrl: "http://items.magischer.de/api/products" ,
        products: [],
        res: null,
      }
    },
    methods: {

      getDataFromApiUrl(url = this.apiUrl) {
        axios.get(url, {
          params: { 
            limit: this.limit, 
            lang: this.lang 
          }
          }).then((response) => { 
          this.res = response.data 
          this.products = response.data.data
        })
      },
      nextPage() {
        this.getDataFromApiUrl(this.res?.next_page_url)
      },
      prevPage() {
        this.getDataFromApiUrl(this.res?.prev_page_url)
      },
      firstPage() {
        this.getDataFromApiUrl(this.res?.first_page_url)
      },
      lastPage() {
        this.getDataFromApiUrl(this.res?.last_page_url)
      },
      limitChange(e) {
        this.limit = e.target.value
        this.getDataFromApiUrl()
      },
      changeLang() {
        this.lang = e.target.value
        this.getDataFromApiUrl()
      },
    },
    mounted() {
    this.getDataFromApiUrl()
   }
}
</script>

<template>
  <!-- <h2 class="text-3xl font-bold underline">here {{ apiUrl }}</h2> -->
  <select @change="limitChange">
    <option v-for="amount in range" :key="amount.index" :value="amount">Per Page: {{ amount }}</option>
  </select>
  <br>
  <select @change="changeLang">
    <option v-for="amount in langs" :key="amount.index" :value="amount">Change Language: {{ amount }}</option>
  </select>
  <br>
  <table class="table-auto">
    <thead>
      <th>Product id</th>
      <th>Product name</th>
      <th>cover img</th>
    </thead>
    <tbody>
      <tr v-for="item in products" :key="item.index">
        <td>{{ item.id }}</td>
        <td>{{ item.name }}</td>
        <td>
          <img style="width: 200px; height: auto;" :src="item.img.cover" /> 
        </td>
      </tr>
    </tbody>
  </table>
  <br>
  <div style="display: flex; justify-content: between;">
    <a href="#" :disabled="!res?.first_page_url" @click.prevent="firstPage" >FirstPage</a>
    <button :disabled="!res?.prev_page_url" @click.prevent="prevPage">Prev</button>
    <button :disabled="!res?.next_page_url" @click.prevent="nextPage">Next</button>
    <a href="#" :disabled="!res?.last_page_url" @click.prevent="lastPage" >LastPage</a>
  </div>
</template>