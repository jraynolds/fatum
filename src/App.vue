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
				<v-btn @click="roll">
					<v-icon>mdi-refresh</v-icon>
				</v-btn>
			</v-col>
    </v-app-bar>

    <v-main>
			<v-row class="justify-center mt-4">
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
					<RandomCard 
						:lists="[ classes, backgrounds, bonds ]"
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
					<RandomCard 
						:lists="[ classes, backgrounds, bonds ]"
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
							<RandomCard 
								:colors="chosenEvent1.questions[0].colors"
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
							<RandomCard 
								:colors="chosenEvent1.questions[1].colors"
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
							<RandomCard 
								:colors="chosenEvent1.questions[2].colors"
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
							v-if="chosenEvent2.questions && chosenEvent2.questions.length"
							v-show="event2Shown"
						>
							<RandomCard 
								:colors="chosenEvent2.questions[0].colors"
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
							<RandomCard 
								:colors="chosenEvent2.questions[1].colors"
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
							<RandomCard 
								:colors="chosenEvent2.questions[2].colors"
								:slotTitle="chosenEvent2.questions[2].name"
								:small="true" 
							/>
						</v-col>
					</v-row>
				</v-col>

			</v-row>
    </v-main>
  </v-app>
</template>

<script>
import cards from "@/assets/cards.json"
import Card from "@/components/Card.vue"
import RandomCard from "@/components/RandomCard.vue"

export default {
  name: 'App',
  components: {
		Card,
		RandomCard
  },
  data: () => ({
    cards,
		chosenPlace: null,
		chosenClass: null,
		chosenBackground: null,
		chosenBond1: null,
		chosenBond2: null,
		chosenEvent1: null,
		chosenEvent2: null,
		
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
		roll() {
			this.chosenPlace = this.getRandomElement(this.places);
			this.chosenClass = this.getRandomElement(this.classes);
			this.chosenBackground = this.getRandomElement(this.backgrounds);
			this.chosenBond1 = this.getRandomElement(this.bonds);
			this.chosenBond2 = this.getRandomElement(this.bonds);
			this.chosenEvent1 = this.getRandomElement(this.events);
			this.chosenEvent2 = this.getRandomElement(this.events);
			this.event1Shown = false;
			this.event2Shown = false;
			this.bond1Shown = false;
			this.bond2Shown = false;
		}
	},
	beforeMount() {
		this.roll();
	},
};
</script>

<style>
.dualwidth {
	width: fit-content;
}
</style>