<template>
  <div class="container">
    <booking-selects v-model="bookingInfo" />
    <booking-inputs v-model="bookingInfo" />
  </div>
</template>

<script>
export default {
  name: 'BookingComponent',
  data() {
    return {
      bookingInfo: {
        selectedFlightType: 'round-trip',
        passengers: 0,
        selectedTravelClass: 'economy',
        origin: '',
        destiny: '',
        departureDate: '',
        returnDate: '',
      },
    }
  },
}
</script>

<style lang="scss" scoped></style>
