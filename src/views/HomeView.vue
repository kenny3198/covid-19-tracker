<template>
  <main v-if="!loading">
    <dataTitle :text= "title" :dataDate= "dataDate"/>
    <dataBoxes :stats="stats"/>
    <country-select @get-country="getCountryData" :Countries="Countries"/>
    <button @click="clearCountry" v-if="stats.Country" class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">
      Clear Country
    </button>
  </main>
  <main v-else class="flex flex-col justify-center align-center text-center">
    <div class="text-gray-500 text-3xl mt-1o mb-6">
     
    </div>
    <img :src="loadingImage" class="w-24 m-auto" alt="">
  </main>
</template>

<script>
// @ is an alias to /src
import dataTitle from "@/components/dataTitle"
import dataBoxes from "@/components/dataBoxes"
import countrySelect from "@/components/countrySelect"
export default {
  name: 'HomeView',
  components: { dataTitle, dataBoxes, countrySelect },
  data() {
    return {
    loading: true,
    title: "Global",
    dataDate: "",
    stats: {},
    Countries: [],
    loadingImage: require("../assets/loading.gif")
    }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary')
      const data = await res.json()
      return data
    },
    getCountryData(country) {
    this.stats = country
    this.title = country.Country
    },
    async clearCountry() {
      this.loading = true
      const data = await this.fetchCovidData()
      this.title = "global"
      this.stats = data.Global
      this.loading = false
    }
  },
  async created() {
   const data = await this.fetchCovidData()
   this.dataDate = data.Date
   this.stats = data.Global
   this.Countries = data.Countries
   this.loading = false
   console.log(data)
  }
}
</script>
