<template>
   <headerApp/>
   <div class="container mx-auto">
    <router-view/>
   </div>
 
</template>
<script>
import headerApp from "@/components/headerApp"
export default {
  components: { headerApp}
}
</script>


