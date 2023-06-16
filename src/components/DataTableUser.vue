<template>
	<div>
		<table v-if="filteredData.length">
			<thead>
				<tr>
					<th>Имя</th>
					<th>Фамилия</th>
					<th @click="sortName = !sortName" style="cursor: pointer">
						Никнейм 🔝
					</th>
					<th>Почта</th>
					<th>Аватар</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="item in filteredData" :key="item.uuid">
					<td>{{ item.firstname }}</td>
					<td>{{ item.lastname }}</td>
					<td>{{ item.username }}</td>
					<td>{{ item.email }}</td>
					<td><img :src="item.image" :alt="item.uuid" width="80" /></td>
				</tr>
			</tbody>
		</table>
	</div>
</template>

<script>
	export default {
		props: {
			data: {
				type: Array,
				required: true,
			},
		},
		data() {
			return {
				sortName: false,
			};
		},
		computed: {
			filteredData() {
				let filtered = [...this.data];

				if (this.sortName) {
					filtered = filtered.sort((a, b) => {
						return a.username.localeCompare(b.username);
					});
				}

				return filtered;
			},
		},
	};
</script>
