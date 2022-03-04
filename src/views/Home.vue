<template>
	<v-container>
		<v-row class="justify-center mt-0">
			<v-col class="flex-grow-0">
				<Card 
					:cardObj="chosenPlace"
					:cardList="places" 
					slotTitle="Origins"
					slotDescription="Where did you begin?"
				/>
			</v-col>
			
			<v-col class="flex-grow-0">
				<Card 
					:cardObj="chosenBackground" 
					:cardList="backgrounds" 
					slotTitle="Background"
					slotDescription="What's your story?" 
				/>
			</v-col>
		</v-row>

		<v-row class="justify-center mb-1">
			<v-col class="flex-grow-0 grey" v-show="bond1Shown">
				<Card 
					:cardObj="chosenBond1Answer"
					:cardList="chosenBond1AnswerList" 
					slotTitle="Who?"
					:small="true" 
				/>
			</v-col>

			<v-col class="flex-grow-0 grey">
				<Card 
					:cardObj="chosenBond1" 
					:cardList="bonds" 
					slotTitle="Bond"
					slotDescription="An important person."
					:clicked.sync="bond1Shown" 
				/>
			</v-col>
			
			<v-col class="flex-grow-0">
				<Card 
					:cardObj="chosenClass" 
					:cardList="classes" 
					slotTitle="Class"
					slotDescription="Who are you?" 
				/>
			</v-col>
			
			<v-col class="flex-grow-0 grey">
				<Card 
					:cardObj="chosenBond2" 
					:cardList="bonds" 
					slotTitle="Bond"
					slotDescription="An important person." 
					:clicked.sync="bond2Shown" 
				/>
			</v-col>

			<v-col class="flex-grow-0 grey" v-show="bond2Shown">
				<Card 
					:cardObj="chosenBond2Answer"
					:cardList="chosenBond2AnswerList" 
					slotTitle="Who?"
					:small="true" 
				/>
			</v-col>
		</v-row>

		<v-row class="justify-center">
			<v-col cols="6" class="text-right">
				<v-row 
					class="mr-1" 
					style="flex-direction: row-reverse; margin-left: auto; width: fit-content !important;"
				>
					<v-col class="flex-grow-0 grey" style="width: 208px">
						<Card 
							:cardObj="chosenEvent1" 
							:cardList="events" 
							slotTitle="Storied past"
							slotDescription="What sticks with you?"
							:clicked.sync="event1Shown" 
						/>
					</v-col>

					<v-col 
						class="flex-grow-0 grey" 
						style="width: 165px" 
						v-if="chosenEvent1.questions && chosenEvent1.questions.length"
						v-show="event1Shown"
					>
						<Card 
							:cardObj="event1Answer1"
							:cardList="event1Answer1List" 
							:slotTitle="chosenEvent1.questions[0].name"
							:small="true" 
						/>
					</v-col>
					<v-col 
						class="flex-grow-0 grey" 
						style="width: 165px" 
						v-if="chosenEvent1.questions && chosenEvent1.questions.length > 1"
						v-show="event1Shown"
					>
						<Card 
							:cardObj="event1Answer2"
							:cardList="event1Answer2List" 
							:slotTitle="chosenEvent1.questions[1].name"
							:small="true" 
						/>
					</v-col>
					<v-col 
						class="flex-grow-0 grey" 
						style="width: 165px" 
						v-if="chosenEvent1.questions && chosenEvent1.questions.length > 2"
						v-show="event1Shown"
					>
						<Card 
							:cardObj="event1Answer3"
							:cardList="event1Answer3List" 
							:slotTitle="chosenEvent1.questions[2].name"
							:small="true" 
						/>
					</v-col>
				</v-row>
			</v-col>
			
			<v-col cols="6">
				<v-row 
					class="ml-1 dualwidth"
					:style="$vuetify.breakpoint.lgAndUp ? { } : { width: '372px !important' }"
				>
					<v-col class="flex-grow-0 grey" style="width: 208px">
						<Card 
							:cardObj="chosenEvent2" 
							:cardList="events" 
							slotTitle="Goal"
							slotDescription="What's next?"
							:clicked.sync="event2Shown"
						/>
					</v-col>

					<v-col 
						class="flex-grow-0 grey" 
						style="width: 165px" 
						v-if="chosenEvent2.questions && chosenEvent2.questions.length > 0"
						v-show="event2Shown"
					>
						<Card 
							:cardObj="event2Answer1"
							:cardList="event2Answer1List" 
							:slotTitle="chosenEvent2.questions[0].name"
							:small="true" 
						/>
					</v-col>
					<v-col 
						class="flex-grow-0 grey" 
						style="width: 165px" 
						v-if="chosenEvent2.questions && chosenEvent2.questions.length > 1"
						v-show="event2Shown"
					>
						<Card 
							:cardObj="event2Answer2"
							:cardList="event2Answer2List" 
							:slotTitle="chosenEvent2.questions[1].name"
							:small="true" 
						/>
					</v-col>
					<v-col 
						class="flex-grow-0 grey" 
						style="width: 165px" 
						v-if="chosenEvent2.questions && chosenEvent2.questions.length > 2"
						v-show="event2Shown"
					>
						<Card 
							:cardObj="event2Answer3"
							:cardList="event2Answer3List" 
							:slotTitle="chosenEvent2.questions[2].name"
							:small="true" 
						/>
					</v-col>
				</v-row>
			</v-col>

		</v-row>
	</v-container>
</template>

<script>
import cards from "@/assets/cards.json"
import Card from "@/components/Card.vue"

export default {
  name: 'Home',
  components: {
		Card
  },
  data: () => ({
    cards,
		chosenPlace: null,
		chosenClass: null,
		chosenBackground: null,
		chosenBond1: null,
		chosenBond2: null,

		chosenBond1Answer: null,
		chosenBond1AnswerList: null,
		chosenBond2Answer: null,
		chosenBond2AnswerList: null,

		chosenEvent1: null,
		chosenEvent2: null,

		event1Answer1: null,
		event1Answer1List: null,
		event1Answer2: null,
		event1Answer2List: null,
		event1Answer3: null,
		event1Answer3List: null,

		event2Answer1: null,
		event2Answer1List: null,
		event2Answer2: null,
		event2Answer2List: null,
		event2Answer3: null,
		event2Answer3List: null,
		
		bond1Shown: false,
		bond2Shown: false,
		event1Shown: false,
		event2Shown: false
  }),
	computed: {
		classes() { return this.cards.filter(c => c.name == "class")[0] },
		backgrounds() { return this.cards.filter(c => c.name == "background")[0] },
		bonds() { return this.cards.filter(c => c.name == "bond")[0] },
		events() { return this.cards.filter(c => c.name == "event")[0] },
		places() { return this.cards.filter(c => c.name == "place")[0] },
		randomPlace() {
			return this.getRandomElement(this.places);
		}
	},
	methods: {
		getRandomElement(list) {
			let card = list.cards[Math.floor(Math.random() * list.cards.length)];
			if (card.length) {
				if (Math.random() > .5) return card[0];
				return card[1];
			}
			return card;
		},
		getListsFromColors(colors) {
			let lists = [];
			for (let color of colors) lists.push(this.cards.find(c => c.color == color));
			return lists;
		},
		getRandomElementAndList(lists) {
			let listLength = 0;
			for (let list of lists) listLength += list.cards.length;

			let index = Math.floor(Math.random() * listLength);
			let i = 0;
			let prevI = 0;
			for (let list of lists) {
				i += list.length;
				if (index < i) {
					return { item: list.cards[index - prevI], list };
				}
				prevI = i;
			}
			return { item: lists[0].cards[0], list: lists[0] };
		},
		randomCardFromLists(lists) {
			let i = 0;
			for (let list of lists) {
				let iPrev = i;
				i += list.cards.length;
				if (this.randomNumber >= i) continue; 
				let card = list.cards[this.randomNumber - iPrev]; 
				return card;
			}
			return lists[0].cards[0];
		},
		getStringFromCard(card) {
			let indexFlipAndList = this.getIndexFlipAndListFromCard(card);
			if (!card) return "lxcxfx";
			return `l${this.cards.indexOf(indexFlipAndList.list)}c${indexFlipAndList.index}f${indexFlipAndList.flip}`;
		},
		getIndexFlipAndListFromCard(card) {
			for (let cardList of this.cards) {
				for (let i=0; i<cardList.cards.length; i++) {
					let c = cardList.cards[i];
					if (c == card) return { index: i, flip: 0, list: cardList };
					if (c.length) {
						if (c[0] == card) return { index: i, flip: 0, list: cardList };
						if (c[1] == card) return { index: i, flip: 1, list: cardList };
					}
				}
			}
			return null;
		},
		getListAndCardFromMatch(match) {
			if (match[0] == "x" || match[1] == "x" || match[2] == "x") return { list: null, card: null }
			let list = this.cards[match[2]];
			let card = list.cards[match[3]];
			if (card.length) card = card[match[4]]
			return { list, card };
		},
		roll() {
			let urlString = "";

			this.chosenPlace = this.getRandomElement(this.places);
			urlString += this.getStringFromCard(this.chosenPlace);
			this.chosenClass = this.getRandomElement(this.classes);
			urlString += this.getStringFromCard(this.chosenClass);
			this.chosenBackground = this.getRandomElement(this.backgrounds);
			urlString += this.getStringFromCard(this.chosenBackground);
			let randomElementAndList;
			
			this.chosenBond1 = this.getRandomElement(this.bonds);
			randomElementAndList = this.getRandomElementAndList([
				this.classes, this.backgrounds, this.bonds
			]);
			this.chosenBond1Answer = randomElementAndList.item;
			this.chosenBond1AnswerList = randomElementAndList.list;
			urlString += this.getStringFromCard(this.chosenBond1);
			urlString += this.getStringFromCard(this.chosenBond1Answer);

			this.chosenBond2 = this.getRandomElement(this.bonds);
			randomElementAndList = this.getRandomElementAndList([
				this.classes, this.backgrounds, this.bonds
			]);
			this.chosenBond2Answer = randomElementAndList.item;
			this.chosenBond2AnswerList = randomElementAndList.list;
			urlString += this.getStringFromCard(this.chosenBond2);
			urlString += this.getStringFromCard(this.chosenBond2Answer);

			this.chosenEvent1 = this.getRandomElement(this.events);
			if (this.chosenEvent1.questions[0]) {
				randomElementAndList = this.getRandomElementAndList(this.getListsFromColors(this.chosenEvent1.questions[0].colors));
				this.event1Answer1 = randomElementAndList.item;
				this.event1Answer1List = randomElementAndList.list;
			} 
			if (this.chosenEvent1.questions[1]) {
				randomElementAndList = this.getRandomElementAndList(this.getListsFromColors(this.chosenEvent1.questions[1].colors));
				this.event1Answer2 = randomElementAndList.item;
				this.event1Answer2List = randomElementAndList.list;
			} 
			if (this.chosenEvent1.questions[2]) {
				randomElementAndList = this.getRandomElementAndList(this.getListsFromColors(this.chosenEvent1.questions[2].colors));
				this.event1Answer3 = randomElementAndList.item;
				this.event1Answer3List = randomElementAndList.list;
			} 
			urlString += this.getStringFromCard(this.chosenEvent1);
			urlString += this.getStringFromCard(this.event1Answer1);
			urlString += this.getStringFromCard(this.event1Answer2);
			urlString += this.getStringFromCard(this.event1Answer3);


			this.chosenEvent2 = this.getRandomElement(this.events);
			if (this.chosenEvent2.questions[0]) {
				randomElementAndList = this.getRandomElementAndList(this.getListsFromColors(this.chosenEvent2.questions[0].colors));
				this.event2Answer1 = randomElementAndList.item;
				this.event2Answer1List = randomElementAndList.list;
			} 
			if (this.chosenEvent2.questions[1]) {
				randomElementAndList = this.getRandomElementAndList(this.getListsFromColors(this.chosenEvent2.questions[1].colors));
				this.event2Answer2 = randomElementAndList.item;
				this.event2Answer2List = randomElementAndList.list;
			} 
			if (this.chosenEvent2.questions[2]) {
				randomElementAndList = this.getRandomElementAndList(this.getListsFromColors(this.chosenEvent2.questions[2].colors));
				this.event2Answer3 = randomElementAndList.item;
				this.event2Answer3List = randomElementAndList.list;
			} 
			urlString += this.getStringFromCard(this.chosenEvent2);
			urlString += this.getStringFromCard(this.event2Answer1);
			urlString += this.getStringFromCard(this.event2Answer2);
			urlString += this.getStringFromCard(this.event2Answer3);

			this.event1Shown = false;
			this.event2Shown = false;
			this.bond1Shown = false;
			this.bond2Shown = false;

			this.$router.push("/" + urlString);
		}
	},
	beforeMount() {
		if (!this.$route.params.id) this.roll();
		else {
			let groups = [...this.$route.params.id.matchAll(/(l([\dx]+)c([\dx]+)f([\dx]+))/g)];
			console.log(groups);
			
			this.chosenPlace = this.getListAndCardFromMatch(groups[0]).card,
			this.chosenClass = this.getListAndCardFromMatch(groups[1]).card,
			this.chosenBackground = this.getListAndCardFromMatch(groups[2]).card,
			this.chosenBond1 = this.getListAndCardFromMatch(groups[3]).card,
			this.chosenBond2 = this.getListAndCardFromMatch(groups[5]).card,

			this.chosenBond1Answer = this.getListAndCardFromMatch(groups[4]).card,
			this.chosenBond1AnswerList = this.getListAndCardFromMatch(groups[4]).list,
			this.chosenBond2Answer = this.getListAndCardFromMatch(groups[6]).card,
			this.chosenBond2AnswerList = this.getListAndCardFromMatch(groups[6]).list,

			this.chosenEvent1 = this.getListAndCardFromMatch(groups[7]).card,
			this.chosenEvent2 = this.getListAndCardFromMatch(groups[11]).card,

			this.event1Answer1 = this.getListAndCardFromMatch(groups[8]).card,
			this.event1Answer1List = this.getListAndCardFromMatch(groups[8]).list,
			this.event1Answer2 = this.getListAndCardFromMatch(groups[9]).card,
			this.event1Answer2List = this.getListAndCardFromMatch(groups[9]).list,
			this.event1Answer3 = this.getListAndCardFromMatch(groups[10]).card,
			this.event1Answer3List = this.getListAndCardFromMatch(groups[10]).list,

			this.event2Answer1 = this.getListAndCardFromMatch(groups[12]).card,
			this.event2Answer1List = this.getListAndCardFromMatch(groups[12]).list,
			this.event2Answer2 = this.getListAndCardFromMatch(groups[13]).card,
			this.event2Answer2List = this.getListAndCardFromMatch(groups[13]).list,
			this.event2Answer3 = this.getListAndCardFromMatch(groups[14]).card,
			this.event2Answer3List = this.getListAndCardFromMatch(groups[14]).list
		}
	},
};
</script>

<style>
.dualwidth {
	width: fit-content;
}
</style>