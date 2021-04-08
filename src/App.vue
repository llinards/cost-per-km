<template>
	<div class="container mt-3 p-3 card">
		<h4 class="text-center">🚗 Calculate cost per km for your vehicle. 🚗</h4>
		<label for="fuelConsumption" class="form-label text-center w-100"
			>Your current fuel consumption : {{ fuelConsumption }} l/100 km.⛽️</label
		>
		<input v-model="fuelConsumption" type="range" class="form-range" min="1" max="20" step="0.1" id="fuelConsumption" />
		<label for="pricePerLiter" class="form-label text-center w-100">Price per liter: {{ pricePerLiter }} EUR. 💶</label>
		<input v-model="pricePerLiter" type="range" class="form-range" min="0.01" max="3" step="0.01" id="pricePerLiter" />
		<p class="text-center" v-show="costPerKm">
			One km costs you about: <strong>{{ costPerKm }} EUR. 💶</strong>
		</p>
		<label for="calculateYourTripCosts" class="form-label text-center w-100"
			>Trip: <strong>{{ trip }} km.</strong> This trip will cost you
			<strong>~ {{ pricePerTrip }} EUR. 💶</strong></label
		>
		<input v-model="trip" type="range" class="form-range" min="1" max="2500" step="1" id="calculateYourTripCosts" />
	</div>
</template>

<script>
export default {
	name: "App",
	components: {},
	data() {
		return {
			fuelConsumption: 0,
			pricePerLiter: 0,
			trip: 0,
		};
	},
	computed: {
		costPerKm() {
			return ((1 / 100) * this.fuelConsumption * this.pricePerLiter).toFixed(3);
		},
		pricePerTrip() {
			return ((this.trip / 100) * this.fuelConsumption * this.pricePerLiter).toFixed(2);
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
.card {
	background-color: #ecf0f1;
	box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
	max-width: 760px;
	margin: 0 auto;
	border-radius: 5px;
}
@media (max-width: 768px) {
	.card {
		max-width: 90%;
	}
}
</style>
