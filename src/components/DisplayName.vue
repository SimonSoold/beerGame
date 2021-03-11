<template>
  <div class="name-display">
    <h3>{{ currentPlayers[turnCount].name }}s tur</h3>
    <ul>
      <li v-for="(item, index) in names" v-bind:key="index">
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      names: [],
    };
  },
  watch: {
    turnCount() {
      this.names.push(this.names.shift());
    },
  },
  props: {
    turnCount: Number,
    currentPlayers: Array,
  },
  created() {
    for (let current of this.currentPlayers) {
      this.names.push(current.name);
    }
  },
};
</script>

<style>
.name-display {
  height: fit-content;
  margin: 0 4% 0 4%;
}
.name-display > h3 {
  margin: 0;
  padding: 0.24rem 0.48rem;
  white-space: nowrap;
  cursor: pointer;
  font-size: 2.4rem;
}
.name-display > ul {
  display: none;
  position: absolute;
  background: white;
  font-size: 1.6rem;
  padding: 0.24rem 0.48rem;
  margin: 0;
  min-width: 24vw;
}
.name-display > ul > :first-child {
  display: none;
}
.name-display:hover > ul {
  display: inline;
  z-index: 2;
}
@media only screen and (max-width: 1040px) {
.name-display:hover > ul {
  display: none;
}
}
</style>