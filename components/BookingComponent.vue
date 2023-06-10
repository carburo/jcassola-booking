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
        selectedFlightType: 'one-way',
        selectedTravelClass: 'economy',
      },
    }
  },
}
</script>

<style lang="scss" scoped></style>
