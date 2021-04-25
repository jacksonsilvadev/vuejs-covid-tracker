<template>
  <div>
    <main v-if="!loading"> 
      <div class="text-center mb-5">
        <span class="font-bold">{{ title }}</span>
        <p> {{ getFormatedDate }} </p>
      </div>

      <data-boxes :stats="stats"/>

      <SelectCountry :countries="countries" @update="changeCountry"/>
    
      <button @click="clearData" class="rounded bg-blue-500 text-white p-3 mt-5"> Limpar Filtro </button>
    </main>
    <main class="flex flex-col align-center justify-center text-center" v-else>
      <img :src="loaderImage" class="w-24 m-auto">
    </main>
  </div>
</template>

<script>
import moment from 'moment'
import DataBoxes from '@/components/DataBoxes'
import SelectCountry from '@/components/SelectCountry'

export default {
  name: 'Home',
  components: {
    DataBoxes,
    SelectCountry
  },
  data: () => ({   
    country: '',
    title: 'Global',
    date: '',
    stats: {},
    countries: [],
    loading: true,
    loaderImage: require('../assets/spinner.gif')
  }),
  computed: {
    getFormatedDate(){
      return moment(this.date).format('DD/MM/YYYY hh:mm')
    }
  },
  methods: {
    async fetchData() {
      try {
        this.loading = true    
        const response = await fetch('https://api.covid19api.com/summary')
        const data = response.json()
        return data
      }catch (e) {
        this.loading = false
        console.error(e)    
      }
    },
    changeCountry(countryId) {
      const country = this.countries.find((c) => c.ID === countryId)
      if(country) {
        this.stats = country
        this.title = country.Country
        this.date = country.Date
      }
    },
    async clearData() {
      this.country = ''
      const data = await this.fetchData()

      this.title = 'Global'
      this.stats = data.Global
      this.countries = data.Countries
      this.loading = false
    }
  },
  async created() {
    const data = await this.fetchData();

    this.date = data.Date
    this.stats = data.Global
    this.countries  = data.Countries
    this.loading = false
  }
}
</script>
