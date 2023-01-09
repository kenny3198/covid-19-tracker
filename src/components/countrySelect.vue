<template>
  <select @change="onChange()" v-model="selected" class="form-selected mt-1 block w-full border p-3 rounded">
    <option value="0"> Select Country</option>
    <option v-for="country in Countries" :key="country" :value="country.ID">{{ country.Country }}</option>
  </select>
</template>

<script> 
export default {
props: ["Countries"],
data() {
    return {
        selected: 0
    }
},
methods: {
    onChange() {
        const country = this.Countries.find((item) => item.ID === this.selected)
        this.$emit("get-country", country )
    }
}
}
</script>

<style>

</style>