<template>
	<div>
		<table>
			<thead>
				<tr>
					<th>Тип</th>
					<th>Номер</th>
					<th>Истекает</th>
					<th @click="sortName = !sortName" style="cursor: pointer">
						Пользователь 🔝
					</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="item in filteredData" :key="item.number">
					<td>{{ item.type }}</td>
					<td>{{ item.number }}</td>
					<td>{{ item.expiration }}</td>
					<td>{{ item.owner }}</td>
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
			filterValue: {
				type: String,
				default: '',
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

				filtered = filtered.filter(item => {
					if (this.filterValue) {
						return item.number.includes(this.filterValue);
					}
					return item;
				});

				if (this.sortName) {
					filtered = filtered.sort((a, b) => {
						return a.owner.localeCompare(b.owner);
					});
				}

				return filtered;
			},
		},
	};
</script>
