<template>
	<div class="row">
		<div class="col-6 col-md-3 mt-3" v-if="state.gridConfigured">
			<div class="mb-2 value" v-if="state.gridPower > 0">
				Bezug <fa-icon icon="arrow-down" class="text-primary"></fa-icon>
			</div>
			<div class="mb-2 value" v-else>
				Einspeisung <fa-icon icon="arrow-up" class="text-primary"></fa-icon>
			</div>
			<h2 class="value">
				{{ fmt(state.gridPower) }}
				<small class="text-muted">{{ fmtUnit(state.gridPower) }}W</small>
			</h2>
		</div>
		<div class="col-6 col-md-3 mt-3" v-if="state.pvConfigured">
			<div class="mb-2 value">
				Erzeugung
				<fa-icon
					icon="sun"
					v-bind:class="{
						'text-primary': state.pvPower < 0,
						'text-muted': state.pvPower >= 0,
					}"
				></fa-icon>
			</div>
			<h2 class="value">
				{{ fmt(state.pvPower) }}
				<small class="text-muted">{{ fmtUnit(state.pvPower) }}W</small>
			</h2>
		</div>
		<div class="d-md-block col-6 col-md-3 mt-3" v-if="state.batteryConfigured">
			<div class="mb-2 value">
				Batterie
				<fa-icon
					class="text-primary"
					icon="arrow-down"
					v-if="state.batteryPower < 0"
				></fa-icon>
				<fa-icon
					class="text-primary"
					icon="arrow-up"
					v-if="state.batteryPower > 0"
				></fa-icon>
			</div>
			<h2 class="value">
				{{ fmt(state.batteryPower) }}
				<small class="text-muted">{{ fmtUnit(state.batteryPower) }}W</small>
			</h2>
		</div>
		<div class="col-6 col-md-3 mt-3" v-if="state.batteryConfigured">
			<div class="mb-2 value">
				SoC
				<fa-icon
					icon="battery-three-quarters"
					v-bind:class="{
						'text-primary': state.batteryPower > 0,
						'text-muted': state.batteryPower < 0,
					}"
				></fa-icon>
			</div>
			<h2 class="value">{{ state.batterySoC || 0 }} <small class="text-muted">%</small></h2>
		</div>
	</div>
</template>

<script>
import formatter from "../mixins/formatter";

export default {
	name: "SiteDetails",
	props: ["state"],
	mixins: [formatter],
};
</script>
