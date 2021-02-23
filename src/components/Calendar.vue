<template>
  <div class="main">
    <div class="columns is-centered">
      <b-field class="calendar" label="Select a date">
        <b-datepicker
          class="column is-primary"
          placeholder="Click to select..."
          v-model="dates"
          :show-week-number="true"
          :min-date="minDate"
          range
          inline
        >
          <div class="date-selector">
            <div class="previous" @click.prevent="previous">
              Previous
            </div>
            <div class="next" @click.prevent="next">Next</div>
          </div>
        </b-datepicker>
      </b-field>
    </div>
    {{ dates }}
  </div>
</template>

<script>
import Vue from 'vue'

export default {
  name: 'Calendar',

  data() {
    return {
      dates: [],
      minDate: new Date('2020-01-01T03:00:00.000Z')
    }
  },

  mounted() {
    document.getElementsByClassName('pagination-next')[0].style.visibility =
      'hidden'
    document.getElementsByClassName('pagination-previous')[0].style.visibility =
      'hidden'
  },

  methods: {
    previous() {
      if (this.dates.length) {
        let range = (this.dates[1] - this.dates[0]) / (1000 * 60 * 60 * 24)
        const first = this.dates[0].setDate(this.dates[0].getDate() - range)
        const second = this.dates[1].setDate(this.dates[1].getDate() - range)
        Vue.set(this.dates, 0, new Date(first))
        Vue.set(this.dates, 1, new Date(second))
      }
    },

    next() {
      if (this.dates.length) {
        let range = (this.dates[1] - this.dates[0]) / (1000 * 60 * 60 * 24)
        const first = this.dates[0].setDate(this.dates[0].getDate() + range)
        const second = this.dates[1].setDate(this.dates[1].getDate() + range)
        Vue.set(this.dates, 0, new Date(first))
        Vue.set(this.dates, 1, new Date(second))
      }
    }
  }
}
</script>

<style>
.main {
  margin: 1rem;
}

.calendar > .label {
  font-size: 1.5rem;
  text-align: center;
}

.date-selector {
  display: flex;
  justify-content: space-around;
}

.previous,
.next {
  cursor: pointer;
  color: #7957d5;
  font-weight: bold;
}
</style>
