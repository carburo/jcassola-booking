<template>
  <div class="container">
    <h1>Search hundred of travel sites at once.</h1>
    <div class="selects-container">
      <select v-model="fligtType" name="fligt-type" id="flight-type">
        <option selected="selected" value="one-way">One Way</option>
        <option value="round-trip">Round Trip</option>
        <option value="multi-city">Multi City</option>
        <option value="trip-builder">Trip Builder</option>
      </select>
      <div class="passengers-container">
        <button
          class="passengers-button"
          @click="displayPassengerOptions"
          name="passengers"
          id="passengers"
        >
          {{ totalPassengers }} travelers
        </button>
        <div v-if="showPassengerOptions" class="passengers-options">
          <div
            class="passengers-counter"
            v-for="passenger in passengers"
            :key="passenger.name"
          >
            <div class="name-container">
              <p>
                {{ passenger.name }}<span>{{ passenger.spam }}</span>
              </p>
            </div>
            <div class="passenger-buttons">
              <button @click="decrement(passenger)">-</button>
              <span>{{ passenger.value }}</span>
              <button @click="increment(passenger)">+</button>
            </div>
          </div>
        </div>
      </div>
      <select v-model="travelClass" name="travelClass" id="travelClass">
        <option selected="selected" value="economy">Economy</option>
        <option value="premium-economy">Premium Economy</option>
        <option value="business">Business</option>
        <option value="first">Fist</option>
        <option value="multiple">Multiple</option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BookingComponent',
  data() {
    return {
      showPassengerOptions: false,
      fligtType: 'one-way',
      travelClass: 'economy',
      passengers: [
        { name: 'Adults', spam: '18-64', value: 1 },
        { name: 'Students', spam: 'over 18', value: 0 },
        { name: 'Senior', spam: 'over 65', value: 0 },
        { name: 'Youths', spam: '12-17', value: 0 },
        { name: 'Children', spam: '2-11', value: 0 },
        { name: 'Toddlers in own seat', spam: 'under 2', value: 0 },
        { name: 'Infants on lap', spam: 'under 2', value: 0 },
      ],
      passengersSelected: '1 adult',
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
  },
  methods: {
    increment(passenger) {
      passenger.value++
    },
    decrement(passenger) {
      passenger.value--
    },
    displayPassengerOptions() {
      this.showPassengerOptions = !this.showPassengerOptions
    },
  },
}
</script>

<style lang="scss" scoped>
.selects-container {
  display: flex;
  gap: 10px;
  select {
    border: 0;
  }
}

.passengers-container {
  display: relative;

  .passengers-button {
    padding: 10px;
    border: 0;
  }

  .passengers-options {
    border-radius: 4px;
    box-shadow: 0 10px 20px rgba(25, 32, 36, 0.1),
      0 3px 6px rgba(25, 32, 36, 0.04), 0 -3px 6px rgba(25, 32, 36, 0.04);
    position: absolute;
    margin-left: -100px;
    padding: 32px;
    transition: opacity 100ms ease-in 150ms;

    .passengers-counter {
      display: flex;

      .passenger-buttons {
        button {
          border-radius: 5px;
          border: 1px solid #9ba8b0;
          color: blue;
        }
        span {
          margin: 0 5px;
        }
      }
      .name-container {
        width: 200px;
        span {
          font-size: 10px;
          margin-left: 5px;
        }
      }
    }
  }
}
</style>
