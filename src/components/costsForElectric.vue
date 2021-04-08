<template>
	<div class="container mt-3 mb-5 p-3 card">
		<div class="close-btn">
			<button @click="$emit('toggle-ev')" type="button" class="btn-close" aria-label="Close"></button>
		</div>
		<label for="energyConsumption" class="form-label text-center w-100"
			>Average energy consumption:<br /><strong>{{ energyConsumption }} Wh/km</strong></label
		>
		<input
			v-model="energyConsumption"
			type="range"
			class="form-range"
			min="1"
			max="1000"
			step="1"
			id="energyConsumption"
		/>
		<label for="pricePerWh" class="form-label text-center w-100"
			>Price per kWh:<br />
			<strong>{{ pricePerWh }} EUR</strong></label
		>
		<input v-model="pricePerWh" type="range" class="form-range" min="0.01" max="1" step="0.0001" id="pricePerWh" />
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
	</div>
</template>
<script>
export default {
	name: "CalculateCost",
	props: ["trip"],
	data() {
		return {
			energyConsumption: 165,
			pricePerWh: 0.1045,
		};
	},
	computed: {
		costPerKm() {
			return ((this.energyConsumption / 1000) * this.pricePerWh).toFixed(3);
		},
		pricePerTrip() {
			return (this.costPerKm * this.trip).toFixed(2);
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
.close-btn {
	display: flex;
	justify-content: flex-end;
	padding-bottom: 0.5rem;
}
@media (max-width: 768px) {
	.card {
		max-width: 90%;
	}
}
</style>
