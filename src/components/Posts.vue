<template>
</template>

<script>
import { ref, computed } from "vue";
export default {
	name: 'Posts',
	props: {
	},
	setup() {
		const data = ref(null);
		const loading = ref(true);
		const error = ref(null);

		function fetchData() {
			// Will be implemented next
		}

		onMounted(() => {
			fetchData();
		});

		return {
			data,
			loading,
			error
		};
	}
}
</script>