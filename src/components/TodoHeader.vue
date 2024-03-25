<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
	<header class="w-full px-5 md:px-48 bg-zinc-100">
		<nav class="w-full py-5 flex justify-between">
			<div class="flex items-center gap-3">
				<img src="../assets/Vue_Logo_Black.png" alt="vue-logo" class="size-10"/>
				<h1 class="font-sans text-2xl font-bold">Vue Todos</h1>
			</div>
			<ul class="flex gap-6 items-center">
				<RouterLink to="/" class="text-xl">Home</RouterLink>
				<RouterLink to="/about" class="text-xl">About</RouterLink>
			</ul>
		</nav>
	</header>
</template>
