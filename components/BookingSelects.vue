<template>
  <div>
    <h1 class="title">Search hundred of travel sites at once.</h1>
    <div class="selects-container mb-3">
      <select
        v-model="bookingInfo.selectedFlightType"
        name="fligt-type"
        id="flight-type"
        class="select"
      >
        <option
          v-for="flightType in flightTypes"
          :key="flightType.name"
          :value="flightType.value"
          class="option"
        >
          {{ flightType.name }}
        </option>
      </select>
      <div class="passengers-container">
        <button
          class="passengers-button"
          @click="togglePassengerOptions"
          name="passengers"
          id="passengers"
        >
          {{ passengersText }}
          <i
            style="font-size: 0.9em"
            class="fas fa-chevron-down float-right"
          ></i>
        </button>
        <div v-if="showPassengerOptions" class="passengers-options">
          <div
            class="passengers-counter"
            v-for="passenger in passengers"
            :key="passenger.name"
          >
            <div class="passenger-name-container">
              <p class="passenger-name">
                {{ passenger.name
                }}<span class="passenger-spam">{{ passenger.spam }}</span>
              </p>
            </div>
            <div class="passenger-buttons">
              <button
                :disabled="passenger.value === 0"
                @click="decrement(passenger)"
                class="passenger-button passenger-button--decrement"
              >
                -
              </button>
              <span>{{ passenger.value }}</span>
              <button
                class="passenger-button passenger-button--increment"
                @click="increment(passenger)"
              >
                +
              </button>
            </div>
          </div>
        </div>
      </div>
      <select
        v-model="bookingInfo.selectedTravelClass"
        name="travelClass"
        id="travelClass"
        class="select"
      >
        <option
          v-for="travelClass in travelClasses"
          :key="travelClass.name"
          :value="travelClass.value"
          class="option"
        >
          {{ travelClass.name }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BookingSelects',
  props: {
    value: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      showPassengerOptions: false,
      flightTypes: [
        { name: 'One Way', value: 'one-way' },
        { name: 'Round Trip', value: 'round-trip' },
        { name: 'Multi City', value: 'multi-city' },
        { name: 'Trip Builder', value: 'trip-builder' },
      ],
      travelClasses: [
        { name: 'Economy', value: 'economy' },
        { name: 'Premium Economy', value: 'premium-economy' },
        { name: 'Business', value: 'business' },
        { name: 'First', value: 'first' },
        { name: 'Multiple', value: 'multiple' },
      ],

      passengers: [
        { name: 'Adults', spam: '18-64', value: 1 },
        { name: 'Students', spam: 'over 18', value: 0 },
        { name: 'Senior', spam: 'over 65', value: 0 },
        { name: 'Youths', spam: '12-17', value: 0 },
        { name: 'Children', spam: '2-11', value: 0 },
        { name: 'Toddlers in own seat', spam: 'under 2', value: 0 },
        { name: 'Infants on lap', spam: 'under 2', value: 0 },
      ],
      passengersSelected: 1,
    }
  },
  computed: {
    totalPassengers() {
      let totalPassengers = 0
      this.passengers.forEach((passenger) => {
        totalPassengers += passenger.value
      })
      return totalPassengers
    },
    passengersText() {
      const total = this.totalPassengers
      if (total === 1) {
        const passenger = this.passengers.find((p) => p.value > 0)
        if (passenger) {
          const name = passenger.name.toLowerCase()
          if (name === 'adults') {
            return '1 adult'
          } else {
            return '1 child'
          }
        }
      }
      return `${total} travellers`
    },
    bookingInfo: {
      get() {
        return this.value
      },
      set(val) {
        this.$emit('input', val)
      },
    },
  },

  watch: {
    totalPassengers(val) {
      this.bookingInfo.passengers = val
    },
  },
  methods: {
    increment(passenger) {
      passenger.value++
    },
    decrement(passenger) {
      passenger.value--
    },
    togglePassengerOptions() {
      this.showPassengerOptions = !this.showPassengerOptions
      document.addEventListener('click', this.hidePassengerOptions)
    },
    hidePassengerOptions(event) {
      if (!this.$el.contains(event.target)) {
        this.showPassengerOptions = false
        document.removeEventListener('click', this.hidePassengerOptions)
      }
    },
  },
}
</script>

<style lang="scss" scoped>
.selects-container {
  display: flex;
  gap: 10px;
  .select {
    border: 0;
  }
}

.passengers-container {
  display: relative;

  .passengers-button {
    background: transparent;
    padding: 10px;
    border: 0;
  }

  .passengers-options {
    border-radius: 4px;
    box-shadow: 0 10px 20px rgba(25, 32, 36, 0.1),
      0 3px 6px rgba(25, 32, 36, 0.04), 0 -3px 6px rgba(25, 32, 36, 0.04);
    position: absolute;
    background: #fff;
    z-index: 100;
    margin-left: -100px;
    padding: 32px;

    .passengers-counter {
      display: flex;

      .passenger-buttons {
        .passenger-button {
          border-radius: 5px;
          border: 1px solid #9ba8b0;
        }
        span {
          margin: 0 5px;
        }
      }
      .passenger-name-container {
        width: 200px;
        .passenger-spam {
          font-size: 10px;
          margin-left: 5px;
        }
      }
    }
  }
}

@media screen and (max-width: 500px) {
  .title {
    font-size: 24px;
    text-align: center;
  }
}
</style>
