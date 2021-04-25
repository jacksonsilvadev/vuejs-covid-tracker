<template>
  <div class="grid grid-cols-2">
    <div class="text-center shadow-md bg-blue-100 p-10">
      <h4 class="text-blue-900 font-bold"> Casos </h4>
      <div>
        <span class="font-bold"> Novos: </span>
        {{ stats.NewConfirmed }}
      </div>
      <div>
        <span class="font-bold"> Total: </span>
        {{ stats.TotalConfirmed }}
      </div>
    </div>
    <div class="text-center shadow-md bg-blue-300 p-10"> 
      <h4 class="text-blue-900 font-bold"> Mortes </h4>
      <div>
        <span class="font-bold"> Novas: </span>
        {{ stats.NewDeaths }}
      </div>
      <div>
        <span class="font-bold"> Total: </span>
        {{ stats.TotalDeaths }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    stats: {
      type: Object,
      default: () => ({})
    }
  }

}
</script>

<style>

</style>