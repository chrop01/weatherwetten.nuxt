<template>
  <v-footer app color="black"> <!-- padless -->
    <v-col
      class="text-center"
      cols="12"
    >
      {{ new Date().getFullYear() }} — <strong>Weather Wetten</strong>
    </v-col>
  </v-footer>
</template>

<script>
import NavBar from "@/components/NavBar";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },components: {
    NavBar
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
