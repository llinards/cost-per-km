<template>
	<div class="main-app">
		<h3 class="text-center mt-3">Calculate the cost per km/trip for your vehicle.</h3>
		<costsForFossilFuel :text="isVisible" :trip="trip" @trip-change="tripChange" @toggle-ev="toggleEv" />
		<costsForElectric v-if="isVisible" @toggle-ev="toggleEv" :trip="trip" @trip-change="tripChange" />
	</div>
</template>

<script>
import costsForFossilFuel from "./components/costsForFossilFuel";
import costsForElectric from "./components/costsForElectric";
export default {
	name: "App",
	components: {
		costsForFossilFuel,
		costsForElectric,
	},
	data() {
		return {
			isVisible: false,
			trip: 100,
		};
	},
	methods: {
		tripChange(trip) {
			this.trip = trip;
		},
		toggleEv() {
			this.isVisible = !this.isVisible;
		},
	},
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap");
h1,
h2,
h3,
h4,
h5,
h6,
p,
label,
a {
	font-family: "Montserrat", sans-serif;
}
body {
	background-color: #bdc3c7;
}
.main-app {
	display: flex;
	justify-content: center;
	align-content: center;
	flex-direction: column;
	height: 100vh;
	width: 100%;
}
</style>
