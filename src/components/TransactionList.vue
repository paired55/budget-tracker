<template>
	<h3>History</h3>
	<ul id="list" class="list">
		<li v-for="item in transactions" :class="transactionClass(item)">
			{{ item.text || "Unknown" }} <span>{{ item.amount }} EGP</span>
		</li>
	</ul>
</template>

<script setup>
	import { defineProps, ref, computed } from "vue";

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
</script>
