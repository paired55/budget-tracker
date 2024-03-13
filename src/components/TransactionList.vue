<template>
	<h3>History</h3>
	<p v-if="transactions.length === 0">No transactions yet</p>
	<ul id="list" class="list">
		<li
			v-for="item in transactions"
			:class="transactionClass(item)"
			:key="item.id"
		>
			{{ item.text || "Unknown" }} <span>{{ item.amount }} EGP</span>
			<button @click="removeTransaction(item.id)" class="delete-btn">x</button>
		</li>
	</ul>
</template>

<script setup>
	import { defineProps, ref, computed } from "vue";

	const emit = defineEmits(["transactionDeleted"]);

	const props = defineProps({
		transactions: {
			type: Array,
			required: true,
		},
	});

	const transactionClass = computed(() => {
		return (item) => {
			return item.amount < 0 ? "minus" : "plus";
		};
	});

	const removeTransaction = (id) => {
		emit("transactionDeleted", id);
	};
</script>
