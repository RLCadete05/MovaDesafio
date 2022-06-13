<template>
  <div class="mt-2">
    <FlagsInfo class="mb-10" :card="country"/>
    <span style="font-size: 18px;">Países Vizinhos</span>
    <div class="container-cards">
      <FlagsCards
        v-for="item in paginatedItems"
        :key="item.name"
        :card="item"
      />
    </div>
    <div class="container-pagination">
      <v-pagination
        class="pagination"
        color="#6D2080"
        v-model="pagination.page"
        :length="pagination.total"
        :total-visible="pagination.visible"
      ></v-pagination>
    </div>
  </div>
</template>

<script>
import FlagsCards from '../../components/Flags/FlagsCards.vue'
import FlagsInfo from '../../components/Flags/FlagsInfo.vue'
export default {
  components: { FlagsInfo, FlagsCards },

  data () {
    return {
      name: this.$route.params.name,
      pagination: {
        page: 1,
        total: 0,
        perPage: 12,
        visible: 7
      },
      country: {},
      borders: []
    }
  },

  async created () {
    await this.getCountry()
  },
  methods: {
    async getCountry () {
      try {
        const response = await this.$axios.$get(`/alpha/${this.name}`)

        this.country = response[0]

        if (this.country.borders) {
          const items = this.country.borders
          for (let i = 0; i < items.length; i++) {
            let response = await this.$axios.$get(`/alpha/${items[i]}`)
            this.borders.push(response[0]);
          }
        }

        this.pagination.total = Math.ceil(
          this.borders.length / this.pagination.perPage
        )
      } catch (error) {
        throw new Error(error)
      }
    }
  },
  computed: {
    paginatedItems () {
      let page = this.pagination.page - 1
      const perPage = this.pagination.perPage
      let start = page * perPage
      let end = start + perPage

      const paginatedItems = this.borders

      return paginatedItems.slice(start, end)
    }
  }
}
</script>

<style scoped>
.container-cards {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  max-width: 100%;
  margin-top: 20px;
}

.container-pagination {
  width: 100%;
  display: flex;
  justify-content: center;
}

.pagination {
  position: fixed;
  bottom: 0;
  margin-bottom: 20px;
}
</style>
