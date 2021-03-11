<template>
  <div
    v-if="value < 11"
    class="middle"
    v-bind:class="{ middleThree: value < 4 }"
  >
  <middlePattern class="img-middle" v-bind:type="cardType" v-bind:value="cardValue"/>
  </div>
  <div class="img-middle" v-else>
      <img :src="imgLink" alt="" >
  </div>

</template>

<script>
import middlePattern from "@/components/cardMiddlePattern.vue";
export default {
  data() {return {

  }},
  props: {
    value: Number,
    imgLink: String,
    color: String,
    type: String
  }, components: {
    middlePattern
  },
  computed: {
    cardType() {
      return this.type
    }, 
    cardValue() {
      return this.value
    }
  },
  methods: {
    gridRow(index) {
      if (this.value > 8) {
        switch (index) {
          case 5:
            return "2/3";
          case 6:
            return "2/3";
          case 7:
            return "3/4";
          case 8:
            return "3/4";
          case 9:
            return "1/3";
          case 10:
            return "3/5";
        }
      }
      if (this.value > 5) {
        switch (index) {
          case 5:
            return "2/4";
          case 6:
            return "2/4";
          case 7:
            return "1/3";
          case 8:
            return "3/5";
        }
      }
      if (this.value > 3) {
        switch (index) {
          case 1:
            return "1/2";
          case 2:
            return "4/5";
          case 3:
            return "1/2";
          case 4:
            return "4/5";
          case 5:
            return "2/4";
        }
      }
    },
    gridColumn(index) {
      if (this.value > 8) {
        switch (index) {
          case 7:
            return "1/2";
          case 8:
            return "3/4";
          case 9:
            return "2/3";
          case 10:
            return "2/3";
        }
      }
      if (this.value > 5) {
        switch (index) {
          case 5:
            return "1/2";
          case 6:
            return "3/4";
        }
      }
      if (this.value > 3) {
        switch (index) {
          case 1:
            return "1/2";
          case 2:
            return "1/2";
          case 3:
            return "3/4";
          case 4:
            return "3/4";
          case 5:
            return "2/3";
        }
      }
    },
  },
};
</script>

<style>
.img-small {
  display: flex;
  justify-content: center;
  align-items: center;
}
.img-small > img {
  max-width: 65%;
  max-height: 100%;
  margin: 0;
}
.middle {
  box-sizing: border-box;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(4, 25%);
  grid-auto-flow: column;
  justify-items: center;
}
.middle > img {
  max-width: 50%;
  max-height: 100%;
  justify-self: center;
}
.img-middle {
  grid-row: 1/5;
  grid-column: 1/4;
  display: flex;
  justify-content: center;
  align-items: center;
}
.img-middle > img {
  max-width: 100%;
  max-height: 100%;
}
.middleThree {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
}
.middleThree > .img-small {
  width: 48%;
}

</style>