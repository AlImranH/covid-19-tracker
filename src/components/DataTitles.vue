<template>
  <div class="text-center">
      <h2 class="text-3xl font-bold">{{ text }}</h2>
      <div class="text-2xl mb-10 mt-4">{{ timestamp }}</div>
  </div>
</template>

<script>
import moment from 'moment'
export default {
    name: "DataTitles",
    props:['text', 'dataDate'],
    computed: {
        timestamp() {
            return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a');
        }
    },
}

</script>

<style>

</style>