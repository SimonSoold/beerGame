<template>
  <div class="rule-display">
    <p>Regler</p>
    <ul class="rule-display-list">
      <li v-for="item in currentRules" v-bind:key="item">{{ item }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    currentRules: Array,
  },
};
</script>

<style>
.rule-display {
  height: fit-content;
  text-align: left;
}
.rule-display > ul {
  display: none;
  position: absolute;
  background: white;
  font-size: 1.6rem;
  padding: 0.24rem 0.48rem;
  margin: 0;
}
.rule-display > p {
  margin: 0;
  padding: 0.24rem 0.48rem;
  white-space: nowrap;
  cursor: pointer;
  font-size: 2.4rem;
}
.rule-display:hover > ul {
  width: 100%;
  display: inline;
  z-index: 2;
}
@media only screen and (max-width: 1040px) {
  .rule-display > p {
  font-size: 1.6rem;
}
.rule-display > ul {
  font-size: 1.6rem;
}
}
</style>