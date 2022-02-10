<template>
  <select v-model="selected" class="form-select block border mt-10 rounded w-full p-1" @change="onChange">
      <option value="0">Select Country</option>
      <option v-for="country in countries" :value="country.ID" :key="country.CountryCode">{{ country.Country }}</option>
  </select>
</template>

<script>
export default {
    name: "CountrySelect",
    props: ["countries"],
    data() {
        return {
            selected: 0
        }
    },
    methods: {
        onChange() {
            const country = this.countries.find((c) => c.ID === this.selected)
            console.log(country);
            this.$emit('getCountry', country)
        }
    },
}
</script>

<style>

</style>