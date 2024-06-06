<template>
	<header>
		<img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

		<h1>Vite + Vue</h1>
		<nav>
			<RouterLink to="/">Home</RouterLink>
			<RouterLink to="/about">About</RouterLink>
		</nav>
	</header>

	<RouterView />
</template>

<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>
