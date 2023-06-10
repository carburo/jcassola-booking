<template>
  <div class="row travel-inputs w-100">
    <div class="d-flex origin-and-destiny-container mb-2">
      <div class="input-group origin">
        <div class="input-group-prepend">
          <span class="input-group-text"><i class="fas fa-plane"></i></span>
        </div>
        <input
          type="text"
          class="form-control"
          id="origin"
          placeholder="From ?"
        />
      </div>

      <button class="p-1 switcher">
        <span class="input-group-text"
          ><i class="fas fa-exchange-alt"></i
        ></span>
      </button>

      <div class="input-group destiny">
        <div class="input-group-prepend">
          <span class="input-group-text"><i class="fas fa-plane"></i></span>
        </div>
        <input
          type="text"
          class="form-control"
          id="destiny"
          placeholder="To ?"
        />
      </div>
    </div>

    <div class="d-flex dates-container mb-2">
      <div class="input-group d-flex dates">
        <div class="input-group date departure-date">
          <div class="input-group-prepend">
            <span class="input-group-text"
              ><i class="fas fa-calendar"></i
            ></span>
          </div>
          <input type="date" class="form-control" id="departure-date" />
        </div>
        <span
          v-if="!(bookingInfo.selectedFlightType === 'one-way')"
          class="separator"
        ></span>
        <div
          v-if="!(bookingInfo.selectedFlightType === 'one-way')"
          class="input-group date return-date"
        >
          <div class="input-group-prepend">
            <span class="input-group-text"
              ><i class="fas fa-calendar"></i
            ></span>
          </div>
          <input type="date" class="form-control" id="return-date" />
        </div>
      </div>
    </div>

    <div class="d-grid d-md-flex search-button-container">
      <button class="btn me-md-2" type="button">
        <i class="fas fa-search"></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BookingInputs',
  props: {
    value: {
      type: Object,
      default: () => {},
    },
  },
  computed: {
    bookingInfo: {
      get() {
        return this.value
      },
    },
  },
}
</script>

<style lang="scss" scoped>
.input-group-text {
  height: 100%;
  border: none;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}
input {
  padding: 15px 0;
  background-color: #e9ecef;
  border: 0;
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
  &:focus {
    border: none;
    box-shadow: none;
    background-color: #e9ecef;
  }
}
.input-group:focus-within {
  outline: 1px solid black;
  border-radius: 8px;
}
.input-group:hover {
  input,
  .input-group-text {
    background-color: #d1d2d3;
  }
}

.switcher {
  border: none;
  border-radius: 8px;
  &:hover {
    background-color: #d1d2d3;
  }
}

.origin-and-destiny-container {
  position: relative;
  width: 50%;
  gap: 10px;
}
.dates-container {
  width: 45%;
  gap: 10px;
  .separator {
    border: 2px solid #b9bbbd;
  }
}
.dates .date {
  flex-basis: 43%;
  flex-grow: 1;
}
.departure-date input {
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}
.return-date .input-group-text {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}

.search-button-container {
  width: 5%;
  height: 51px;
  button {
    background: linear-gradient(135deg, #ff690f 0%, #e8381b 100%);
    border-radius: 10px;
    color: white;
  }
}

@media screen and (max-width: 1024px) {
  .origin-and-destiny-container {
    width: 100%;
  }
  .dates-container,
  .search-button-container,
  .search-button-container button {
    width: 100%;
  }
}
@media screen and (max-width: 500px) {
  .d-flex {
    flex-direction: column;
  }
  .date {
    margin-bottom: 5px !important;
  }
  .separator {
    display: none;
  }
  .switcher {
    position: absolute;
    border: 4px solid #fff;
    top: 27px;
    right: 31px;
    z-index: 20;
  }
}
</style>
