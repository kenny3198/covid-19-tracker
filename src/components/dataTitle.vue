<template>
  <div class="text-center">
  <h2 class="text-3xl font-bold"> {{ text}}</h2>
  <div class="text-2xl mt-4 mb-10">
    {{dataDate}}
  </div>
  </div>
</template>

<script>
import moment from "moment"
export default { 
  props: ["text", "dataDate"],
  computed: {
    timestamp: function() {
        return moment(this.dataDate).format("MMM Do YYY, h:mm:ss a")
    }
  }
}
</script>

<style>

</style>