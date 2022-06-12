<template>
  <div>
    <v-btn
      elevation="2"
      width="136"
      class="font-weight-regular text-capitalize hidden-sm-and-down"
      outlined
      tile
      color="#6D2080"
      @click="toHome"
    >
      <img src="../assets/Vector.svg" alt="Icon Arrow Back" class="mr-5">
      Voltar
    </v-btn>
    <v-btn
      elevation="0"
      width="40"
      class="font-weight-regular text-capitalize hidden-sm-and-up"
      @click="toHome"
    >
      <img src="../assets/Vector.svg" alt="Icon Arrow Back">
    </v-btn>
  </div>
</template>

<script>
export default {
  name: 'BackButton',
  methods: {
    toHome() {
      this.$router.push({ path: '/' })
    }
  }
}
</script>
