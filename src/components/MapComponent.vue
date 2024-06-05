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

	/**
	 * ? Agregar Capa Grafica
	 * Una capa gráfica es un contenedor de gráficos.
	 * Se utiliza con una vista de mapa para mostrar gráficos en un mapa.
	 * Puede añadir más de una capa de gráficos a una vista de mapa.
	 * Las capas de gráficos se muestran encima de todas las demás capas.
	 */
	const graphicsLayer = new GraphicsLayer()
	map.add(graphicsLayer)

	/**
	 * ? Agregar un punto grafico
	 * Un gráfico de puntos se crea utilizando un punto y un símbolo de marcador.
	 * Un punto se define con coordenadas de longitud (x) y latitud (y), y un símbolo simple se define con un color y un contorno.
	 * Las clases Point y SimpleMarkerSymbol se utilizan para crear el gráfico de puntos.
	 *
	 * Ref: [Point](https://developers.arcgis.com/javascript/latest/api-reference/esri-geometry-Point.html)
	 * Ref: [SimpleMarkerSymbol](https://developers.arcgis.com/javascript/latest/api-reference/esri-symbols-SimpleMarkerSymbol.html)
	 */
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
