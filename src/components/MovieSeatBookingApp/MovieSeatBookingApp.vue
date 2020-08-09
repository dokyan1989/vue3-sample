<template>
  <div class="movie-seat-booking-body">
    <MovieSelectForm v-bind:movies="movies" v-model="selectedMoviePrice" />
    <MovieShowCase />
    <MovieSeatList v-bind:seats="seats" v-on:seat-select="handleSeatSelect" />
    <MovieSelectedResult v-bind:count="count" v-bind:total="total" />
  </div>
</template>

<script>
import MovieShowCase from './MovieShowCase.vue'
import MovieSeatList from './MovieSeatList.vue'
import MovieSelectForm from './MovieSelectForm.vue'
import MovieSelectedResult from './MovieSelectedResult.vue'

export default {
  name: 'MovieSeatBookingApp',
  components: {
    MovieShowCase,
    MovieSeatList,
    MovieSelectForm,
    MovieSelectedResult,
  },
  data() {
    return {
      selectedMoviePrice: 12,
      movies: [
        { id: 1, name: 'Avengers: Endgame', price: 10 },
        { id: 2, name: 'Joker', price: 12 },
        { id: 3, name: 'Toy Story 4', price: 8 },
        { id: 4, name: 'The Lion King', price: 9 },
      ],
      seats: [
        { id: 1, availableStatus: 0 },
        { id: 2, availableStatus: 0 },
        { id: 3, availableStatus: 0 },
        { id: 4, availableStatus: 0 },
        { id: 5, availableStatus: 0 },
        { id: 6, availableStatus: 0 },
        { id: 7, availableStatus: 0 },
        { id: 8, availableStatus: 0 },
        { id: 9, availableStatus: 0 },
        { id: 10, availableStatus: 0 },
        { id: 11, availableStatus: 0 },
        { id: 12, availableStatus: 2 },
        { id: 13, availableStatus: 2 },
        { id: 14, availableStatus: 0 },
        { id: 15, availableStatus: 0 },
        { id: 16, availableStatus: 0 },
        { id: 17, availableStatus: 0 },
        { id: 18, availableStatus: 0 },
        { id: 19, availableStatus: 0 },
        { id: 20, availableStatus: 0 },
        { id: 21, availableStatus: 0 },
        { id: 22, availableStatus: 0 },
        { id: 23, availableStatus: 2 },
        { id: 24, availableStatus: 2 },
        { id: 25, availableStatus: 0 },
        { id: 26, availableStatus: 0 },
        { id: 27, availableStatus: 0 },
        { id: 28, availableStatus: 0 },
        { id: 29, availableStatus: 0 },
        { id: 30, availableStatus: 0 },
        { id: 31, availableStatus: 0 },
        { id: 32, availableStatus: 0 },
        { id: 33, availableStatus: 0 },
        { id: 34, availableStatus: 0 },
        { id: 35, availableStatus: 0 },
        { id: 36, availableStatus: 2 },
        { id: 37, availableStatus: 2 },
        { id: 38, availableStatus: 0 },
        { id: 39, availableStatus: 0 },
        { id: 40, availableStatus: 0 },
        { id: 41, availableStatus: 0 },
        { id: 42, availableStatus: 0 },
        { id: 43, availableStatus: 0 },
        { id: 44, availableStatus: 0 },
        { id: 45, availableStatus: 2 },
        { id: 46, availableStatus: 2 },
        { id: 47, availableStatus: 2 },
        { id: 48, availableStatus: 0 },
      ],
    }
  },
  computed: {
    count() {
      const selectedSeats = this.seats.filter(
        (seat) => seat.availableStatus === 1
      )
      return selectedSeats.length
    },
    total() {
      return this.count * this.selectedMoviePrice
    },
  },
  created() {
    const selectedSeats = JSON.parse(localStorage.getItem('selectedSeats'))
    if (selectedSeats !== null && selectedSeats.length > 0) {
      this.seats.forEach((seat) => {
        if (
          selectedSeats.findIndex((selectedSeat) => seat.id === selectedSeat) >
          -1
        ) {
          seat.availableStatus = 1
        }
      })
    }

    const selectedMoviePrice = localStorage.getItem('selectedMoviePrice')
    this.selectedMoviePrice = selectedMoviePrice ? selectedMoviePrice : 10
  },
  methods: {
    handleSeatSelect(id, status) {
      const seatIndex = this.seats.findIndex((seat) => seat.id === id)
      if (seatIndex > -1) {
        this.seats[seatIndex].availableStatus = status
        const seatsIndex = this.seats
          .filter((seat) => seat.availableStatus === 1)
          .map((seat) => seat.id)
        localStorage.setItem('selectedSeats', JSON.stringify(seatsIndex))
      }
    },
  },
}
</script>

<style scoped>
.movie-seat-booking-body {
  background-color: #242333;
  color: #fff;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-family: 'Lato', sans-serif;
  margin: 0;
}
</style>