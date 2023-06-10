<template>
  <div>
    <h1>Search hundred of travel sites at once.</h1>
    <div class="selects-container mb-3">
      <select v-model="selectedFlightType" name="fligt-type" id="flight-type">
        <option
          v-for="fligtType in flightTypes"
          :key="fligtType.name"
          :value="fligtType.value"
        >
          {{ fligtType.name }}
        </option>
      </select>
      <div class="passengers-container">
        <button
          class="passengers-button"
          @click="displayPassengerOptions"
          name="passengers"
          id="passengers"
        >
          {{ totalPassengers }} travelers
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
      <select v-model="selectedTravelClass" name="travelClass" id="travelClass">
        <option
          v-for="travelClass in travelClasses"
          :key="travelClass.name"
          :value="travelClass.value"
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
  data() {
    return {
      showPassengerOptions: false,
      selectedFlightType: 'one-way',
      selectedTravelClass: 'economy',
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
        button {
          border-radius: 5px;
          border: 1px solid #9ba8b0;
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
