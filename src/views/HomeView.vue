<template>
  <div class="home">
    <GrillaApp msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
import GrillaApp from '@/components/GrillaApp.vue'

export default {
  name: 'HomeView',
  components: {
    GrillaApp,
  },
}
</script>
