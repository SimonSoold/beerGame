<template>
  <div class="Home">
    <h1 v-on:click="tjohej()" class="top-layer">Välkommen till Ölspelet</h1>
    <InputPlayer class="top-layer"/>
    <Bubblor class="bubblor" v-bind:startCount="0" />
    <Bubblor class="bubblor2" v-bind:startCount="7" />
    <Bubblor class="bubblor3" v-bind:startCount="2" />
  </div>
</template>

<script>
// @ is an alias to /src
import InputPlayer from "@/components/InputPlayer.vue";
import Bubblor from "@/components/Bubblor.vue";

export default {
  name: "Home",
  components: {
    InputPlayer,
    Bubblor,
  }
};
</script>
<style>
.Home {
  background: #f5d00d;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-template-rows: 20% 1fr 1fr 1fr 20%;
  perspective: 385px;
}
.bubblor {
  z-index: 1;
  grid-row: 1/end;
  grid-column: 1/8;
}
.bubblor2 {
    z-index: 1;
  grid-row: 1/end;
  grid-column: 7/end;
}
.bubblor3 {
    z-index: 1;
  grid-row: 1/4;
  grid-column: 7/10;
}
.Home > h1 {
  grid-row: 1/2;
  grid-column: 1/13;
  text-align: center;
  font-size: 4.8rem;
}
.Home > .input-player {
  z-index: 2;
  grid-column: 5/9;
  grid-row: 2/5;
  justify-items: center;
  align-items: center;
}
.top-layer {
  z-index: 4;
}

@media only screen and (max-width: 1040px) {
  .Home > h1 {
  grid-row: 1/2;
  grid-column: 2/12;
  text-align: center;
  font-size: 4rem;
}
  .Home {
    grid-template-rows: auto 1fr 2fr 2fr 2fr 2fr 5%;
  }
  .Home > .input-player {
    grid-column: 2/12;
    grid-row: 3/end;
  }
}
@media only screen and (max-width: 600px) {
    .Home > h1 {
  grid-row: 1/2;
  grid-column: 3/11;
  text-align: center;
  font-size: 2.8rem;
}
  .Home {
    grid-template-rows: auto 1fr 2fr 2fr 2fr 10%;
  }
  .Home > .input-player {
    grid-column: 3/11;
    grid-row: 3/end;
  }
  
}
</style>
