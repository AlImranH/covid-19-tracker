<template>
  <main v-if="!loading">
    <DataTitles :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats"/>
    <CountrySelect @getCountry="getCountryData" :countries="countries"/>

    <button @click="clearCountryData" v-if="stats.Country" class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">
      Clear Country
    </button>
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" class="w-24 m-auto" alt="">
  </main>
</template>

<script>
import DataTitles from '@/components/DataTitles'
import DataBoxes from '@/components/DataBoxes'
import CountrySelect from '@/components/CountrySelect'
export default {
  name: 'Home',
  components: {
    DataTitles, DataBoxes, CountrySelect
  },
  data() {
    return {
      loading: true,
      title: "Global",
      countries: [],
      dataDate: '',
      stats: {},
      loadingImage: require('../assets/blue-hourglass.gif')
    }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary')
      const data = res.json()
      return data
    },
    getCountryData(country) {
      this.stats = country
      this.title = country.Country
    },
    async clearCountryData() {
      this.loading = true
      const data = await this.fetchCovidData()
      this.title = "Global"
      this.stats = data.Global
      this.loading = false
    },
  },
  async created() {
    const data = await this.fetchCovidData()
    this.dataDate = data.Date,
    this.countries = data.Countries
    this.stats = data.Global
    this.loading = false
  }
}
</script>
