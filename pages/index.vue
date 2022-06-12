<template>
  <div>
    <FilterGroup class="filter " @getCountry="getData" />
    <div class="container-cards">
      <FlagsCard
        v-for="card in paginatedItems"
        :key="card.name.common"
        :card="card"
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
import FilterGroup from '../components/Filters/FilterGroup.vue'
import FlagsCard from '../components/Flags/FlagsCards.vue'

export default {
  name: 'IndexPage',
  data () {
    return {
      cards: [],
      region: this.$route.query.region,
      pagination: {
        page: 1,
        total: 0,
        perPage: 12,
        visible: 7
      }
    }
  },
  components: {
    FilterGroup,
    FlagsCard,
  },
async mounted () {
    if (this.region) {
      await this.getRegion()
    } else {
      await this.getAll()
    }
  },
  methods: {
    async getAll () {
      try {
        const response = await this.$axios.$get('/all')

        this.cards = response
        this.pagination.total = Math.ceil(
          this.cards.length / this.pagination.perPage
        )
      } catch (error) {
        throw new Error(error)
      }
    },
    async getData (selected, selectedName) {
      try {
        const response = await this.$axios.$get(`/${selected}/${selectedName}`)

        this.$router.push({ path: '/' })

        this.cards = null
        this.cards = response
        this.pagination.total = Math.ceil(
          this.cards.length / this.pagination.perPage
        )
      } catch (error) {
        throw new Error(error)
      }
    },
    async getRegion () {
      try {
        const response = await this.$axios.$get(`/region/${this.region}`)

        this.cards = null
        this.cards = response
        this.pagination.total = Math.ceil(
          this.cards.length / this.pagination.perPage
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

      const paginatedItems = this.cards

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
    min-width: 100%;
    display: flex;
    justify-content: center;
  }

  .pagination {
    position: fixed;
    bottom: 0;
    margin-bottom: 20px;
  }

  @media screen and (min-width: 320px) and (max-width: 600px) {
    .filter {
      display: none !important;
    }
  }
</style>
