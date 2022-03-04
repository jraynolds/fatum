<template>
	<v-app>
		<v-app-bar
			app
			color="primary"
			dark
		>
			<v-col cols="4">
			</v-col>
			<v-col cols="4" class="text-center">
				<h1>Fatum</h1>
			</v-col>
			<v-col cols="4" class="text-right">
				<v-btn @click="$router.push('/').then(() => $router.go('/'))">
					<v-icon>mdi-refresh</v-icon>
				</v-btn>
			</v-col>
		</v-app-bar>

		<v-main>
			<router-view>
			</router-view>
		</v-main>
	</v-app>
</template>

<script>
export default {

}
</script>

<style>

</style>