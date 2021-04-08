<template>
	<div class="container mt-3 p-3 card">
		<label for="fuelConsumption" class="form-label text-center w-100"
			>Average fuel consumption:<br /><strong>{{ fuelConsumption }} l/100 km</strong></label
		>
		<input v-model="fuelConsumption" type="range" class="form-range" min="1" max="20" step="0.1" id="fuelConsumption" />
		<label for="pricePerLiter" class="form-label text-center w-100"
			>Price per liter:<br /><strong>{{ pricePerLiter }} EUR</strong></label
		>
		<input v-model="pricePerLiter" type="range" class="form-range" min="0.01" max="3" step="0.01" id="pricePerLiter" />
		<p class="text-center" v-show="costPerKm">
			1 km costs <strong>~ {{ costPerKm }} EUR.</strong>
		</p>
		<label for="calculateYourTripCosts" class="form-label text-center w-100"
			>Trip: <strong>{{ trip }} km.</strong></label
		>
		<input
			v-model="trip"
			@change="$emit('trip-change', trip)"
			type="range"
			class="form-range"
			min="1"
			max="2500"
			step="1"
			id="calculateYourTripCosts"
		/>
		<p class="text-center mb-0">
			This trip will cost you <strong>~ {{ pricePerTrip }} EUR.</strong>
		</p>
		<div class="button-bar text-center">
			<button v-show="!text" @click="$emit('toggle-ev')" class="btn btn-success">
				{{ text ? "" : "Compare with EV" }}
			</button>
		</div>
	</div>
</template>
<script>
export default {
	name: "CalculateCost",
	props: ["trip", "text"],
	data() {
		return {
			fuelConsumption: 7,
			pricePerLiter: 1.2,
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
	methods: {
		showCalculationsForEv() {
			this.$emit("toggle-ev", this.trip);
		},
	},
};
</script>
<style scoped>
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
