<template>
  <div class="beer">
    <div class="liquid" v-bind:style="{ height: LiquidHeight + '%' }">
      <div></div>
      <div>
        <Bubblor v-bind:startCount="6" />
      </div>
    </div>
  </div>
</template>

<script>
import Bubblor from "@/components/Bubblor.vue";
export default {
  data() {
    return {};
  },
  computed: {
    LiquidHeight() {
      return (this.cardCount / 52) * 100;
    },
  },
  props: {
    cardCount: Number,
  },
  components: {
    Bubblor,
  },
};
</script>

<style>
.beer {
  height: 100%;
  width: 100%;
  border: 0.24rem solid #000000;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-template-rows: repeat(8, 1fr);
}
.liquid {
  align-self: end;
  grid-row: 1/9;
  grid-column: 1/13;
  display: flex;
  flex-direction: column;
  width: 100%;
}
.liquid > :first-child {
  background: white;
  height: 20%;
  width: 100%;
}
.liquid > :nth-child(2) {
  background: #f5d00d;
  height: 80%;
  width: 100%;
}


@media only screen and (max-width: 1040px) {
  .liquid > :first-child {
  background: none;
}
}
@media only screen and (max-width: 600px) {

}
</style>