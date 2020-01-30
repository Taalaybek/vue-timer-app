<template>
	<v-container fluid>
		<v-layout>
			<v-flex xs12 pa-3>
				<v-card>
					<v-card-title class="secondary white--text font-weight-light display-2 text-uppercase justify-center">
						{{ timer }}
					</v-card-title>

					<v-card-text>
						<v-list>
							<v-list-item v-ripple :disabled="state=='running'" class="success mb-3 pointer">
								<v-list-item-content @click="$emit('start')">
									<v-list-item-title>
										<span class="white--text font-weight-bold text-uppercase">Start</span>
									</v-list-item-title>
								</v-list-item-content>
							</v-list-item>
							<v-list-item v-ripple :disabled="state=='stopped' || state=='paused'" class="info mb-3 pointer">
								<v-list-item-content @click="$emit('lap')">
									<v-list-item-title>
										<span class="white--text font-weight-bold text-uppercase">Lap</span>
									</v-list-item-title>
								</v-list-item-content>
							</v-list-item>
							<v-list-item v-ripple :disabled="state=='stopped' || state=='paused'" class="warning mb-3 pointer">
								<v-list-item-content @click="$emit('pause')">
									<v-list-item-title>
										<span class="white--text font-weight-bold text-uppercase">Pause</span>
									</v-list-item-title>
								</v-list-item-content>
							</v-list-item>
							<v-list-item v-ripple class="blue-grey darken-1 mb-3 pointer">
									<v-list-item-content @click="$emit('goOn')">
										<v-list-item-title>
											<span class="white--text font-weight-bold text-uppercase">Continue</span>
										</v-list-item-title>
									</v-list-item-content>
								</v-list-item>
							<v-list-item v-ripple :disabled="state=='stopped'" class="error pointer">
								<v-list-item-content @click="$emit('stop')">
									<v-list-item-title>
										<span class="white--text font-weight-bold text-uppercase">Stop</span>
									</v-list-item-title>
								</v-list-item-content>
							</v-list-item>
						</v-list>
					</v-card-text>
				</v-card>
			</v-flex>
		</v-layout>
	</v-container>
</template>

<script>
export default {
	name: 'timer',
	props: ['timer', 'state']
}
</script>

<style scoped>
	.pointer {
		cursor: pointer
	}
	.none {
		cursor: none
	}
</style>