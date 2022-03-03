<template>
	<Card 
		:cardObj="randomCard"
		:cardList="randomCardList"
		:slotTitle="slotTitle"
		:small="small"
	/>
</template>

<script>
import Card from "@/components/Card.vue"
import cards from "@/assets/cards.json"

export default {
	props: [
		"lists",
		"colors",
		"slotTitle",
		"small"
	],
	components: {
		Card
	},
	data: () => ({
		randomNumber: 0,
		cards
	}),
	computed: {
		cardLists() {
			if (this.lists) return this.lists;
			let lists = [];
			if (this.colors) {
				for (let color of this.colors) {
					lists = lists.concat(this.cards.find(c => c.color == color));
				}
			}
			return lists;
		},
		randomCard() {
			let i = 0;
			for (let list of this.cardLists) {
				let iPrev = i;
				i += list.cards.length;
				if (this.randomNumber >= i) continue; 
				let card = list.cards[this.randomNumber - iPrev]; 
				return card;
			}
			return this.cardLists[0].cards[0];
		},
		randomCardList() {
			let i = 0;
			for (let list of this.cardLists) {
				i += list.cards.length;
				if (this.randomNumber < i) return list;
			}
			return this.cardLists[0].cards[0];
		}
	},
	beforeMount() {
		let listLength = 0;
		for (let list of this.cardLists) listLength += list.cards.length;
		this.randomNumber = Math.floor(Math.random() * listLength);
	}
}
</script>

<style>

</style>