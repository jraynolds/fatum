<template>
	<v-card color="black" dark class="text-center" :class="small ? 'px-2' : 'px-4'">
		<v-card-title class="pa-1 d-flex justify-center" style="word-break: break-word">{{ slotTitleCased }}</v-card-title>
		<VueFlip
			:height="height + 'px'" 
			:width="width + 'px'" 
			active-click 
			:style="{width: `${width}px`}"
			v-model="cardClicked"
		>
			<template v-slot:front>
				<v-card 
					:width="width"
					light 
					:height="height" 
					:color="cardList.color"
					class="d-flex align-center justify-center"
				>
					<v-icon style="font-size: xxx-large">{{ "mdi-" + cardList.icon }}</v-icon>
				</v-card>
			</template>
			<template v-slot:back>
				<v-card 
					:width="width"
					light 
					:height="height" 
					:color="cardList.color"
					class="d-flex align-center justify-center"
				>
					<v-card-title class="text-center" style="word-break: break-word" :style="small ? { fontSize: 'small' } : {}">
						{{ title }}
					</v-card-title>
				</v-card>
			</template>
		</VueFlip>
		<v-card-text class="pa-1">{{ slotDescription }}</v-card-text>
	</v-card>
</template>

<script>
import VueFlip from "vue-flip"

export default {
	props: [
		"cardObj",
		"cardList",
		"slotTitle",
		"slotDescription",
		"small",
		"clicked"
	],
	components: {
		VueFlip
	},
	data: () => ({
		widths: [ 150, 125 ],
		heights: [ 180, 150 ],
		localClicked: false,
	}),
	computed: {
		card() {
			if (this.cardObj.length) {
				if (Math.random() > .5) return this.cardObj[0];
				return this.cardObj[1];
			}
			return this.cardObj;
		},
		cardClicked: {
			get() { 
				if (this.clicked != null) return this.clicked;
				return this.localClicked; 
			},
			set(val) {
				if (this.clicked != null) this.$emit("update:clicked", val);
				this.localClicked = val;
			}
		},
		slotTitleCased() {
			return this.slotTitle.substr(0, 1).toUpperCase() + this.slotTitle.substr(1, this.slotTitle.length);
		},
		title() {
			return this.card.name.substr(0, 1).toUpperCase() + this.card.name.substr(1, this.card.name.length);
		},
		width() {
			if (this.small) return this.widths[1];
			return this.widths[0];
		},
		height() {
			if (this.small) return this.heights[1];
			return this.heights[0];
		}
	}
}
</script>

<style>

</style>