<template>
  <v-app dark class="app">
   <top-bar></top-bar>
    <v-main>
      <v-container fluid>
        <nuxt />
      </v-container>
    </v-main>
    <Footer></Footer>
  </v-app>
</template>


<script>
import TopBar from '@/components/Topbar'
import Footer from  '@/components/Footer.vue'
export default {
  components: {
    TopBar,
    Footer
  },
  data() {
    return {

    }
  },
}
</script>
<style>
 .app{
  font-family: 'Prompt',Prompt;
} 
</style>