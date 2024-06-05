<template>
	<main>
		<h1>Hello World!</h1>

		<div id="viewDiv"></div>
	</main>
</template>

<script setup lang="ts">
import { onMounted } from 'vue'
import esriConfig from '@arcgis/core/config'
import Map from '@arcgis/core/Map'
import MapView from '@arcgis/core/views/MapView'

import Graphic from '@arcgis/core/Graphic'
import GraphicsLayer from '@arcgis/core/layers/GraphicsLayer'

// eslint-disable-next-line no-undef
import esri = __esri

// Establecer la apiKey para habilitar arcGIS
esriConfig.apiKey = import.meta.env.VITE_ARCGIS_API_KEY

onMounted(() => {
	// Creamos mapa base con el estilo topografico
	const map = new Map({
		basemap: 'arcgis/topographic'
	})

	// Creamos la vista para mostrar donde se ubicara el mapa
	const view = new MapView({
		map,
		center: [-118.805, 34.027], // Longitude, latitude
		zoom: 13, // Zoom level
		container: 'viewDiv' // Div element
	})

	// Agregar Capa Grafica
	const graphicsLayer = new GraphicsLayer()
	map.add(graphicsLayer)

	// Agrega un grafico de Punto
	const point = {
		// Creando el punto
		type: 'point',
		longitude: -118.80657463861,
		latitude: 34.0005930608889
	}

	const simpleMarkerSymbol = {
		// Creando el marcador simple
		type: 'simple-marker',
		color: [226, 119, 40], // Orange
		outline: {
			color: [255, 255, 255], // White
			width: 1
		}
	}

	// Cree un gráfico y defina las propiedades de geometría y símbolo.
	const pointGraphic = new Graphic({
		geometry: point as esri.Point,
		symbol: simpleMarkerSymbol
	})
	graphicsLayer.add(pointGraphic)

	// Agrega un grafico de Linea
	const polyline = {
		type: 'polyline',
		paths: [
			[
				[-118.821527826096, 34.0139576938577], // Longitude, Latitude
				[-118.814893761649, 34.0080602407843], // Longitude, Latitude
				[-118.808878330345, 34.0016642996246] // Longitude, Latitude
			]
		]
	}

	const simpleLineSymbol = {
		type: 'simple-line',
		color: [226, 119, 40], // Orange
		width: 2
	}

	// Crea un gráfico y establece las propiedades de geometría y símbolo.
	const polylineGraphic = new Graphic({
		geometry: polyline as esri.Polyline,
		symbol: simpleLineSymbol
	})
	graphicsLayer.add(polylineGraphic)

	// Agregar un grafico poligonal
	const polygon = {
		type: 'polygon',
		rings: [
			[
				[-118.818984489994, 34.0137559967283], // Longitude, latitude
				[-118.806796597377, 34.0215816298725], // Longitude, latitude
				[-118.791432890735, 34.0163883241613], // Longitude, latitude
				[-118.79596686535, 34.008564864635], // Longitude, latitude
				[-118.808558110679, 34.0035027131376] // Longitude, latitude
			]
		]
	}

	const simpleFillSymbol = {
		type: 'simple-fill',
		color: [227, 139, 79, 0.8], // Orange, opacity 80%
		outline: {
			color: [255, 255, 255],
			width: 1
		}
	}

	// Crear una ventana emergente

	/**
	 * Puede mostrar una ventana emergente para un gráfico cuando se hace clic sobre él.
	 * El código que crea el gráfico poligonal para mostrar una ventana emergente
	 * con el nombre y la descripción del gráfico utiliza las propiedades attribute y popupTemplate.
	 */
	const popupTemplate = {
		title: '{Name}',
		content: '{Description}'
	}

	const attributes = {
		Name: 'Graphic',
		Description: 'I am a polygon'
	}

	/**
	 * Actualiza el polygonGraphic para incluir el popupTemplate y las propiedades de los atributos.
	 */

	// Crea un gráfico y establece las propiedades de geometría y símbolo.
	const polygonGraphic = new Graphic({
		geometry: polygon as esri.Polygon,
		symbol: simpleFillSymbol,

		attributes,
		popupTemplate
	})
	graphicsLayer.add(polygonGraphic)
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
