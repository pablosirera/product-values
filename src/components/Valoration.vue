<template>
  <div class="valoration-card">
    <p class="valoration-card__stars">
      <Stars />{{ review.rating.toFixed(1) }}
    </p>
    <p class="valoration-card__name">{{ nameDate }}</p>
    <p>{{ review.comment }}</p>
    <div class="valoration-card__votes">
      <button :class="buttonClass" @click="updateUsefulCount()">
        <img
          class="button__icon"
          :src="require('@/assets/icons/like.png')"
          alt="Like icon"
        />
        Es útil
      </button>
      <span>{{ usefulCountData }}</span>
    </div>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'Valoration',
  components: {
    Stars: () => import('@/components/Stars.vue')
  },
  props: {
    review: {
      type: Object,
      required: true
    }
  },
  computed: {
    nameDate() {
      moment.locale('es')
      const date = this.review.date
      const nameDay = moment(date).format('dddd')
      const day = moment(date).format('DD')
      const month = moment(date).format('MMMM')
      const year = moment(date).format('YYYY')
      const formattedDate = `${nameDay}, ${day} de ${month} de ${year}`

      return `${this.review.author} el ${formattedDate}`
    },
    usefulCountData() {
      const textBelieve = this.review.isVoted ? 'creéis' : 'creen'
      return `${this.review.useful_count} personas ${textBelieve} que es útil`
    },
    buttonClass() {
      return {
        button: true,
        'button--voted': this.review.isVoted
      }
    }
  },
  methods: {
    updateUsefulCount() {
      if (!this.review.isVoted) {
        this.$emit('increaseUsefulCount')
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.valoration-card {
  border: 1px solid #e2e2e2;
  border-radius: 4px;
  padding: 10px;

  &__stars {
    display: flex;
    align-items: center;
  }

  &__name {
    font-size: 11px;
  }

  &__votes {
    display: flex;
    align-items: center;
  }
  .button {
    display: flex;
    margin-right: 10px;
    padding: 5px 7px;
    border-radius: 4px;
    font-weight: 600;
    &:focus {
      outline: none;
    }
    &__icon {
      margin-right: 5px;
      width: 12px;
      color: white;
    }

    &--voted {
      background-color: #359436;
      color: white;
      pointer-events: none;
    }
  }
}
</style>
