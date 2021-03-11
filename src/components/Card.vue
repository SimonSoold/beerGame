<template>
  <div class="card" v-on:click="middleToggle()">
      <div class="card-box">
        <p v-bind:style="{ color: cardColor }">{{ cardValue }}</p>
        <div class="img-big-single">
          <img :src="imgLink" />
        </div>
      </div>

      <CardMiddle
        class="cardMiddle"
        v-bind:value="Number(card.value)"
        v-bind:imgLink="imgLink"
        v-bind:color="card.color"
        v-bind:type="card.type"
        v-show="middleDisplay"
      />
      <div class="cardMiddle cardMiddleRules" v-show="!middleDisplay">
        <p>{{ rule }}</p>
        <p v-show="rule.length < 84">{{ rule }}</p>
      </div>
      <div class="card-box">
        <p v-bind:style="{ color: cardColor }">{{ cardValue }}</p>
        <div class="img-big-single">
          <img :src="imgLink" alt="" />
        </div>
      </div>
  </div>
</template>

<script>
import CardMiddle from "@/components/CardMiddle.vue";

export default {
  components: {
    CardMiddle,
  },

  data() {
    return {
      imgLink: require("@/assets/" + this.card.type + ".svg"),
      middleDisplay: true,
    };
  },
  methods: {
    middleToggle() {
      this.middleDisplay = !this.middleDisplay;
    },
  },
  computed: {
    cardValue() {
      switch (Number(this.card.value)) {
        case 11:
          return "kn";
        case 12:
          return "D";
        case 13:
          return "K";
        case 14:
          return "E";
        default:
          return this.card.value;
      }
    }, 
    cardColor() {
      if (this.card.color === "black") {
        return this.card.color
      } else {
        return "#F52D0D"
      }
    }
  },
  name: "Card",
  props: {
    card: Object,
    rule: String,
  },
  watch: {
    card(value) {
      this.middleDisplay = false
      setTimeout(()=>{this.middleDisplay = !this.middleDisplay}, 3500)
      this.imgLink = require("@/assets/" + value.type + ".svg");

    }, 
  }, 
};
</script>

<style>

.card {
  margin: 2.4%;
  background: white;
  border-radius: 2.4%;
  height: 100%;
  width: 100%;
  box-sizing: border-box;
  padding: 0.8%;
  display: grid;
  grid-template-rows: repeat(5, 1fr);
  grid-template-columns: 1fr 60% 1fr;
}

.cardMiddle {
  grid-row: 2/5;
  grid-column: 2/3;
}
.cardMiddleRules {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.cardMiddle > p {
  text-align: center;
  font-size: 1rem;
  margin: auto 0 auto 0;
}
.cardMiddle > p:nth-child(2) {
  transform: rotate(180deg);
  opacity: 37%;
  filter: blur(4px);
}
.card-box:first-of-type {
  grid-column: 1/2;
  grid-row: 1/3;
}
.card-box:last-of-type {
  grid-column: 3/4;
  grid-row: 4/6;
  flex-direction: column;
  transform: rotate(180deg);
}
.img-big-single > img {
  max-width: 100%;
  max-height: 100%;
  margin: 0;
}
.img-big-single {
  display: flex;
  justify-content: center;
  align-items: center;
}
.card > .card-box > p {
  font-size: 2.6rem;
  text-align: center;
  margin: 0;
}
</style>