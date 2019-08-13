<template lang="html">
	<div id="sightingsGrid">
		<div class="sighting" v-for="sighting in sightings">
			<h2>{{ sighting.species }}</h2>
			<p>{{ sighting.location }} on {{ sighting.date|format }}</p>

			<button type="button" class="delete=btn" v-on:click="deleteBird">Delete Sighting</button>
		</div>
	</div>
</template>

<script>
import { eventBus } from '../main';
import BirdsService from '@/services/BirdsService.js';

export default {
	name: "sightings-grid",
	props: ["sightings"],
	filters: {
		format(value){
			return new Date(value).toLocaleString().substring(0, 10);
		}
	},
	methods: {
    deleteBird(){
			BirdsService.deleteBird(this.sightings._id)
			.then(() => eventBus.$emit('bird-deleted', this.sightings._id))
		}
	}
}
</script>

<style lang="css" scoped>
#sightingsGrid {
	display: flex;
	flex-wrap: wrap;
	justify-content: space-evenly;
}

h2 {
	padding: 0;
	margin: 0;
}

.sighting {
	width: 30%;
	background: rgba(255, 255, 255, 0.7);
	margin-bottom: 20px;
	padding: 25px;
}

button {
	color: #fff;
	border: none;
	font-size: 18px;
	padding: 10px;
	margin-top: 10px;
	background: #F55536;
}
</style>
