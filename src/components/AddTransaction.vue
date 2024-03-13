<template>
	<h3>Add New Transaction</h3>
	<form id="form">
		<div class="form-control">
			<label for="text">Description</label>
			<input
				type="text"
				placeholder="eg. groceries, transportation, coffee..."
				id="description"
				v-model="itemDescription"
			/>
		</div>
		<div class="form-control">
			<label for="amount">Amount <br><span class="amountWarning">(Negative = expense, Positive = income)</span></br></label>
			<input
				type="number"
				id="amount"
				placeholder="Enter amount..."
				v-model="itemAmount"
			/>
		</div>
		<button class="btn" @click.prevent="addTheTransaction">
			Add Transaction
		</button>
	</form>
</template>

<script setup>
import { defineProps, ref, computed } from 'vue';

let id = 0;
const itemDescription = ref('');
const itemAmount = ref(null);

const props = defineProps({
	transactions: {
		type: Array,
		required: true,
	},
});

function addTheTransaction() {
	if (itemAmount.value > 0 || itemAmount.value < 0) {
		props.transactions.push({
			id: id++,
			text: itemDescription.value,
			amount: itemAmount.value,
		});
	}
	itemDescription.value = '';
	itemAmount.value = null;
}
</script>
