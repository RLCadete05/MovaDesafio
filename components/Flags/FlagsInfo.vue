<template>
  <div>
    <div class="d-flex" id="card">
      <v-img
        lazy-src="https://picsum.photos/id/11/10/6"
        max-height="258"
        max-width="443"
        :src="card.flags.svg"
      ></v-img>
      <div class="info" style="background-color: transparent !important;">
        <span>Nome: {{ card.name }}</span>
        <span>Capital: {{ card.capital }}</span>
        <span
          >Região:
          <span
            @click="toRegion(card.region)"
            style="text-decoration: underline; color: blue; cursor: pointer;"
            >{{ card.region }}</span
          ></span
        >
        <span>Sub-região: {{ card.subregion }} </span>
        <span>População: {{ card.population }}</span>
        <span
          >Linguas:
          <span
            class="mr-1"
            v-for="(item, index) in card.languages"
            :key="index"
            >{{ item.nativeName }};</span
          ></span
        >
      </div>
    </div>
    <div class="flex-column" id="card-responsive">
      <v-img
        lazy-src="https://picsum.photos/id/11/10/6"
        max-height="198"
        width="100%"
        max-width="296"
        :src="card.flags.svg"
      ></v-img>
      <div class="info" style="background-color: transparent !important;">
        <span>Nome: {{ card.name }}</span>
        <span>Capital: {{ card.capital }}</span>
        <span
          >Região:
          <span
            @click="toRegion(card.region)"
            style="text-decoration: underline; color: blue; cursor: pointer;"
            >{{ card.region }}</span
          ></span
        >
        <span>Sub-região: {{ card.subregion }} </span>
        <span>População: {{ card.population }}</span>
        <span
          >Linguas:
          <span
            class="mr-1"
            v-for="(item, index) in card.languages"
            :key="index"
            >{{ item.name }};</span
          ></span
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FlagsInfo',
  props: {
    card: Object
  },

  methods: {
    toRegion (region) {
      this.$router.push({ path: '/', query: { region: region } })
    }
  }
}
</script>

<style scoped>
.info {
  min-width: 213px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  color: #454545;
  margin-left: 24px;
}

#card-responsive {
  display: none !important;
}

@media screen and (min-width: 320px) and (max-width: 600px) {
  #card {
    display: none !important;
  }

  #card-responsive {
    display: flex !important;
  }

  .info {
    justify-content: space-between;
    height: 242px;
    margin-top: 22px;
    margin-left: 0px;
  }
}
</style>
