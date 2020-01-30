<template>
	<nav>
		<v-toolbar height="50" dark class="secondary">
			<v-app-bar-nav-icon @click="isDrawerOpen = !isDrawerOpen"></v-app-bar-nav-icon>
			<v-toolbar-title class="headline text-uppercase">
				<span class="font-weight-black primary--text">Alex's </span>
				<span class="font-weight-light">Timer</span>
			</v-toolbar-title>
		</v-toolbar>

		<v-navigation-drawer transition="slide-y-transition" absolute temporary dark @click="isDrawerOpen = !isDrawerOpen" v-model="isDrawerOpen">
			<v-toolbar class="secondary">
				<v-toolbar-title class="title">Laps</v-toolbar-title>
				<v-spacer></v-spacer>
				<v-app-bar-nav-icon @click="isDrawerOpen = !isDrawerOpen"></v-app-bar-nav-icon>
			</v-toolbar>
			<v-list>
				<v-list-item v-for="(lap, index) in laps" :key="index">
					<v-list-item-content>
						<v-list-item-title>Lap {{ index + 1 }} {{ lap.formattedTime }}</v-list-item-title>
					</v-list-item-content>
				</v-list-item>
			</v-list>
		</v-navigation-drawer>
	</nav>
</template>

<script>
export default {
	name: 'navbar',

	props: ['laps'],

	data: () => ({
		isDrawerOpen: false
	})
}
</script>