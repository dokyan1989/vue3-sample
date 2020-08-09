<template>
  <div class="container">
    <div class="screen"></div>

    <div v-for="row in seatsRows" v-bind:key="row.id" class="row">
      <div
        class="seat"
        v-for="seat in row.seats"
        v-bind:key="seat.id"
        v-bind:class="getSeatClass(seat.availableStatus)"
        v-on:click="selectSeat(seat)"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MovieSeatList',
  props: {
    seats: Array,
  },
  computed: {
    seatsRows() {
      return this.seats.reduce((data, seat, index) => {
        if (index % 8 !== 0) {
          data[data.length - 1].seats.push(seat)
        } else {
          const row = data.length + 1
          data.push({ id: row, seats: [seat] })
        }
        return data
      }, [])
    },
  },
  methods: {
    selectSeat(seat, event) {
      if (seat.availableStatus !== 2) {
        this.$emit('seat-select', seat.id, seat.availableStatus === 0 ? 1 : 0)
      }
    },
    getSeatClass(availableStatus) {
      switch (availableStatus) {
        case 0:
          return ''
          break
        case 1:
          return 'selected'
          break
        case 2:
          return 'occupied'
          break
        default:
          return ''
      }
    },
  },
}
</script>

<style scoped>
.container {
  perspective: 1000px;
  margin-bottom: 30px;
}

.row {
  display: flex;
}

.screen {
  background-color: #fff;
  height: 70px;
  width: 100%;
  margin: 15px 0;
  transform: rotateX(-45deg);
  box-shadow: 0 3px 10px rgba(255, 255, 255, 0.7);
}

.seat {
  background-color: #444451;
  height: 12px;
  width: 15px;
  margin: 3px;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}

.seat.selected {
  background-color: #6feaf6;
}

.seat.occupied {
  background-color: #fff;
}

.seat:nth-of-type(2) {
  margin-right: 18px;
}

.seat:nth-last-of-type(2) {
  margin-left: 18px;
}

.seat:not(.occupied):hover {
  cursor: pointer;
  transform: scale(1.2);
}
</style>