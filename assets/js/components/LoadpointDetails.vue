<template>
	<div class="row">
		<div class="col-6 col-md-3 mt-3">
			<div class="mb-2 value">
				Leistung
				<fa-icon
					class="text-primary ml-1"
					icon="temperature-low"
					v-if="state.climater == 'heating'"
				></fa-icon>
				<fa-icon
					class="text-primary ml-1"
					icon="temperature-high"
					v-if="state.climater == 'cooling'"
				></fa-icon>
				<fa-icon
					class="text-primary ml-1"
					icon="thermometer-half"
					v-if="state.climater == 'on'"
				></fa-icon>
			</div>
			<h2 class="value">
				{{ fmt(state.chargePower) }}
				<small class="text-muted">{{ fmtUnit(state.chargePower) }}W</small>
			</h2>
		</div>
		<div class="col-6 col-md-3 mt-3">
			<div class="mb-2 value">Geladen</div>
			<h2 class="value">
				{{ fmt(state.chargedEnergy) }}
				<small class="text-muted">{{ fmtUnit(state.chargedEnergy) }}Wh</small>
			</h2>
		</div>

		<div class="col-6 col-md-3 mt-3" v-if="state.range >= 0">
			<div class="mb-2 value">Reichweite</div>
			<h2 class="value">
				{{ state.range }}
				<small class="text-muted">km</small>
			</h2>
		</div>

		<div class="col-6 col-md-3 mt-3" v-else>
			<div class="mb-2 value">Dauer</div>
			<h2 class="value">
				{{ fmtShortDuration(state.chargeDuration) }}
				<small class="text-muted">{{ fmtShortDurationUnit(state.chargeDuration) }}</small>
			</h2>
		</div>

		<div class="col-6 col-md-3 mt-3" v-if="state.soc">
			<div class="mb-2 value">Restzeit</div>
			<h2 class="value">
				{{ fmtShortDuration(state.chargeEstimate) }}
				<small class="text-muted">{{ fmtShortDurationUnit(state.chargeEstimate) }}</small>
			</h2>
		</div>
	</div>
</template>

<script>
import formatter from "../mixins/formatter";

export default {
	name: "LoadpointDetails",
	props: ["state"],
	mixins: [formatter],
	computed: {
		minSoCActive: function () {
			return (
				this.state.connected &&
				this.state.minSoC > 0 &&
				this.state.socCharge < this.state.minSoC
			);
		},
	},
};
</script>
