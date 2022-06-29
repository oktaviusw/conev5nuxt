<template>
  <div class="body">
    <Navbar/>
    <div>hello hello</div>
    {{ route.fullPath }}

  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Navbar from '~/components/Navbar.vue'

export default Vue.extend({
    name: "IndexPage",
    components: { Navbar },
    data() {
    return {
      route: this.$route,
      
    };
  },
})
</script>
