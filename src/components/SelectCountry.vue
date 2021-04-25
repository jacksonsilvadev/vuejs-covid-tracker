<template>
    <select v-model="country" @change="changeCountry" class="border w-full rounded mt-5 p-3"> 
        <option> Selecione o País</option>
        <option v-for="country in countries" :value="country.ID" :key="country.ID">
          {{ country.Country }}  
        </option>
      </select>
</template>

<script>
export default {
  props: ['countries'],
  data: () => ({
    country: ''
  }),
  methods: {
    changeCountry(){
      this.$emite('update', this.country)
    }  
  }
}
</script>

<style>

</style>