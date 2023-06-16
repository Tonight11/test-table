<template>
	<div>
		<TheHeader />
		<div class="container">
			<div class="table" v-if="dataCard.length > 0">
				<div class="table__card">
					<h2 class="table__title">1 таблица карт</h2>
					<UIInput
						type="text"
						text="Фильтр по номеру карты"
						forId="filter"
						v-model.number="filterValue"
					/>
					<DataTable :data="dataCard" :filter-value="filterValue" />
				</div>
				<div class="table__user">
					<h2 class="table__title">2 таблица юзернейм</h2>
					<DataTableUser :data="dataUsername" />
				</div>
			</div>
			<UILoader v-else />
		</div>
		<TheFooter />
	</div>
</template>

<script>
	import TheHeader from './components/TheHeader.vue';
	import DataTable from './components/DataTable.vue';
	import DataTableUser from './components/DataTableUser.vue';
	import axios from 'axios';
	import TheFooter from './components/TheFooter.vue';
	import UIInput from './components/UI/UIInput.vue';
	import UILoader from './components/UI/UILoader.vue';

	export default {
		components: {
			TheHeader,
			DataTable,
			DataTableUser,
			TheFooter,
			UIInput,
			UILoader,
		},
		data() {
			return {
				dataCard: [],
				dataUsername: [],
				filterValue: '',
			};
		},
		async mounted() {
			const getDataCard = this.getData(
				'https://fakerapi.it/api/v1/credit_cards?_quantity=100'
			);
			const getDataUsername = this.getData(
				'https://fakerapi.it/api/v1/users?_quantity=100'
			);
			try {
				const [card, user] = await Promise.all([getDataCard, getDataUsername]);
				this.dataCard = card;
				this.dataUsername = user;
			} catch (error) {
				console.log(error);
			}
		},
		methods: {
			async getData(url) {
				try {
					await new Promise(resolve => setTimeout(resolve, 1000));

					const { data } = await axios.get(url);
					return data.data;
				} catch (error) {
					console.log(error);
				}
			},
		},
	};
</script>

<style scoped>
	.table {
	}
	.table__card {
		margin-bottom: 100px;
	}
	.table__user {
	}
	.table__title {
		margin-bottom: 25px;
	}
</style>
