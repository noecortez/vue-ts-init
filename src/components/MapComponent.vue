<template>
	<main>
		<h1>Hello World!</h1>

		<div id="viewDiv"></div>
	</main>
</template>

<script setup lang="ts">
import { onMounted } from 'vue'
import Map from '@arcgis/core/Map'
import MapView from '@arcgis/core/views/MapView'
import esriConfig from '@arcgis/core/config'

// Establecer la apiKey para habilitar arcGIS
esriConfig.apiKey = import.meta.env.VITE_ARCGIS_API_KEY

onMounted(() => {
	// Creamos mapa base con el estilo topografico
	const map = new Map({
		basemap: 'arcgis/topographic'
	})

	// Creamos una clase de MapView para estabecer la ubicacion del mapa
	// a mostrar. En este MapView establece la propiedad map.
	// Para centrar la vista del mapa, establezca la propiedad center
	// y establecemos propiedad zoom a 13. Establece la propiedad container
	// al identificador del elemento HTML para colocar el mapa
	const view = new MapView({
		map,
		center: [-118.805, 34.027], // Longitude, latitude
		zoom: 13, // Zoom level
		container: 'viewDiv' // Div element
	})
})
</script>

<style scoped>
/* @import 'https://js.arcgis.com/4.29/@arcgis/core/assets/esri/themes/light/main.css'; */
@import 'https://js.arcgis.com/4.29/@arcgis/core/assets/esri/themes/dark/main.css';

#viewDiv {
	height: 350px;
	margin: 0 auto;
	padding: 0;
	width: 80%;
}
</style>
