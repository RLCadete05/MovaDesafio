<template>
<div>
    <v-app-bar class="hidden-sm-and-down" fixed app height="80">
      <div class="ml-6">
        <NuxtLink to="/"
          ><img
            src="../assets/logo_principal.svg" 
            alt="Logo Mova"
            class="mr-4"
        /></NuxtLink>
      </div>
      <v-spacer />
      <back-button class="mr-6" />
    </v-app-bar>
    <v-app-bar class="hidden-xs-and-up" fixed app height="80">
      <div >
        <NuxtLink to="/"
          ><img
            src="../assets/logo_principal.svg" 
            alt="Logo Mova"
            class="mr-4"
        /></NuxtLink>
      </div>
      <v-spacer />
      <back-button />
    </v-app-bar>
  </div>
</template>

<script>
import BackButton from '../components/BackButton.vue'

export default {
    name: 'Header',
    components: {
        BackButton
    }
}
</script>