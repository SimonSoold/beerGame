<template>
  <div
    class="game"
    v-bind:style="{
      filter: 'blur(' + (60 - currentDeck.length) / 512 + 'rem)',
    }"
  >
    <div class="menu">
      <DisplayName
        v-bind:currentPlayers="currentPlayers"
        v-bind:turnCount="turnCount"
        v-show="newRule && currentDeck.length != 0"
      />
      <p v-show="!newRule && currentDeck.length != 0">Skriv in en regel</p>
      <p v-show="currentDeck.length === 0">Spelet är slut</p>
      <div class="menu-nav">
        <a v-on:click="goToilett()" v-show="currentPlayers[turnCount].tokens > 0 && newRule" href="#">Gå på Toa</a>
        <DisplayRules
          v-bind:currentRules="currentRules"
          v-if="currentRules.length > 0"
        />
        <a
          v-if="currentDeck.length > 0 && newRule"
          v-on:click="newCard()"
          href="#"
          >Nytt kort</a
        >
        <RegelInput
          v-else-if="currentCard.value === 6 && newRule === false"
          @clicked="onClickChild"
        />
        <router-link v-else to="/">Nytt spel</router-link>
      </div>
    </div>
    <Card v-bind:card="currentCard" v-bind:rule="getRules()" />
    <Beer class="beer" v-bind:cardCount="currentDeck.length" />
  </div>
</template>
<script>
import Card from "@/components/Card.vue";
import DisplayName from "@/components/DisplayName.vue";
import DisplayRules from "@/components/DisplayRules.vue";
import RegelInput from "@/components/RegelInput.vue";
import Beer from "@/components/Beer.vue";
// @ is an alias to /src

export default {
  data() {
    return {
      currentCard: { value: "14", type: "clubs", color: "black" },
      currentDeck: [],
      rules: [],
      currentRules: [],
      currentPlayers: [],
      turnCount: 0,
      newRuleInput: "",
      endGame: false,
      newRule: true,
    };
  },
  components: {
    Card,
    DisplayName,
    DisplayRules,
    RegelInput,
    Beer,
  },
  methods: {
    newCard() {
      if (this.turnCount < this.currentPlayers.length - 1) {
        this.turnCount++;
      } else {
        this.turnCount = 0;
      }
      this.currentCard = this.currentDeck.pop();
      if (this.currentCard.value === 6) {
        this.newRule = false;
      } else if (this.currentCard.value === 9) {
        this.currentPlayers[this.turnCount].tokens += 1;
      }
    },
    writeRule(value) {
      this.currentRules.push(value);
    },
    shuffleDeck() {
      //this.currentDeck = require("@/assets/Deck")
      this.createDeck()
      for (let current of this.currentDeck) {
        let randomValue = Math.floor(Math.random() * Math.floor(52));
        let temp = current;
        current = this.currentDeck[randomValue];
        this.currentDeck[randomValue] = temp;
      }
    },
    createDeck() {
      const types = ["spade", "clubs", "heart", "diamond"]
      for (let i = 0; i < 13; i++) {
        for (let j = 0; j < 4; j++) {
          if (j < 2) {
            this.currentDeck.push({"value":(i+2),"type":types[j],"color":"black"})
          } else {
            this.currentDeck.push({"value":(i+2),"type":types[j],"color":"red"})
          }
        }
      }
    },
    getRules() {
      if (
        Number(this.currentCard.value) > 2 &&
        Number(this.currentCard.value) < 6
      ) {
        if (this.currentCard.color == "black") {
          return "Ge bort " + this.currentCard.value + " klunkar till...";
        } else {
          return "Drick " + this.currentCard.value + " klunkar.";
        }
      }
      return this.rules.find(
        (element) => element.name == this.currentCard.value
      ).rule;
    },
    onClickChild(value) {
      this.writeRule(value);
      this.newRule = true;
    }, 
    goToilett() {
      this.currentPlayers[this.turnCount].tokens -= 1
    }
  },
  created() {
    if (!sessionStorage.getItem("Players")) {
      this.$router.push("/");
    }
    this.currentPlayers = JSON.parse(sessionStorage.getItem("Players"));
    this.rules = require("@/assets/Rules");
    this.shuffleDeck();
  }
};
</script>

<style>
.game {
  background-color: #0ab53e;
  background-size: cover;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-auto-flow: row;
  grid-template-rows: auto repeat(7, 1fr);
  justify-items: stretch;
  align-items: stretch;
  gap: 24px;
}
.card {
  grid-column: 3/6;
  grid-row: 3/7;
}
.beer {
  grid-column: 8/11;
  grid-row: 3/7;
}
.game > .menu {
  grid-column: 1/13;
  grid-row: 1/2;
  background: white;
  display: flex;
  justify-content: space-between;
  padding: 0 12% 0 12%;
}
.game > .menu > .menu-nav {
  display: flex;
  justify-content: space-evenly;
}
.game > .menu > .menu-nav > a {
  grid-column: 2/3;
  grid-row: 1/2;
  color: black;
  text-shadow: none;
  text-align: center;
  cursor: pointer;
  margin: 0;
  font-size: 2.4rem;
  font-weight: 400;
  padding: 0.24rem 0.48rem;
  text-decoration: none;
  outline: none;
  height: fit-content;
  width: fit-content;
  white-space: nowrap;
}
.game > .menu > .menu-nav > * {
  border-left: 0.08rem solid black;
}
.game > .menu > .menu-nav > :first-child {
  border: none;
}
.menu > p {
  margin: 0;
  padding: 0.24rem 0.48rem;
  white-space: nowrap;
  font-size: 2.4rem;
}

@media only screen and (max-width: 1040px) {
  .game {
    background: #f5d00d;   
  }
  .game {
    grid-template-rows: repeat(8, 1fr);
  }
  .game > .menu {
    grid-row: 10/end;
    flex-direction: column;
    align-items: center;
    background: none;
  }
  .beer {
    grid-row: 1/13;
    grid-column: 1/end;
    align-self: center;
    justify-self: center;
    position: fixed;
    z-index: -1;
  }
.game > .menu > .menu-nav > * {
  border: none;
  border-right: 0.08rem solid black;
}
.game > .menu > .menu-nav > :last-child {
  border: none;
}
  .game > .menu > :first-child {
    border-bottom: 0.08rem solid black;
  }
  .game > .card {
    grid-column: 2/12;
    grid-row: 2/9;
  }
.game > .menu > .menu-nav > a {
  font-size: 1.6rem;
}
}
</style>