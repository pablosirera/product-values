<template>
  <section class="valorations-layout">
    <Valoration
      v-for="(valoration, index) in valorations"
      :key="index"
      :review="valoration"
      @increaseUsefulCount="onIncreaseUsefulCount(index)"
    />
  </section>
</template>

<script>
import axios from 'axios'

export default {
  name: 'ValorationsContainer',
  components: {
    Valoration: () => import('@/components/Valoration.vue')
  },
  data: () => ({
    valorations: []
  }),
  created() {
    this.loadData()
  },
  methods: {
    async loadData() {
      const response = await axios.get('reviews.json')
      this.valorations = response.data.reviews.map(review => {
        review.isVoted = false
        return review
      })
    },
    onIncreaseUsefulCount(valorationIndex) {
      const reviewer = this.valorations[valorationIndex]
      reviewer.useful_count++
      reviewer.isVoted = true
    }
  }
}
</script>

<style lang="scss" scoped>
.valorations-layout {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 30px;

  @media (max-width: 768px) {
    grid-template-columns: 1fr 1fr;
  }

  @media (max-width: 360px) {
    grid-template-columns: 1fr;
  }
}
</style>
