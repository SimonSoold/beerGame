<template>
  <div class="input-player">
    <h2 class="header">Lägg till en spelare</h2>
    <div class="input-player-inputs">
      <input
        type="text"
        placeholder="Namn"
        v-model="currentName"
        v-bind:class="{ error: inputError }"
      />
      <button v-on:click="createPlayer()">Lägg&nbsp;till</button>
    </div>
    <div class="input-player-list">
      <p
        class="input-players-p"
        v-for="(item, index) in playerList"
        v-bind:key="index"
        v-on:click="removePlayer(index)"
      >
        {{ item.name }}
      </p>
    </div>
    <div>
      <router-link
        class="input-player-link"
        v-if="playerList.length > 0"
        to="/BeerGame"
        >Spela</router-link
      >
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentName: "",
      playerList: [],
      inputError: false,
    };
  },
  methods: {
    createPlayer() {
      if (this.currentName.length > 3) {
        this.playerList.push({ name: this.currentName, tokens: 0 });
        sessionStorage.setItem("Players", JSON.stringify(this.playerList));
        this.currentName = "";
      } else {
        this.inputError = !this.inputError;
        setTimeout(() => {
          this.inputError = !this.inputError;
        }, 1000);
      }
    },
    removePlayer(index) {
      this.playerList.splice(index, 1);
    },
  },
  created() {
    if (sessionStorage.getItem("Players")) {
      this.playerList = JSON.parse(sessionStorage.getItem("Players"))
    }
  },
};
</script>

<style>
.input-player {
  background: #ffe14d73;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  cursor: default;
}
.input-player > h2 {
  font-size: 1.6rem;
  text-align: center;
  white-space: nowrap;
}
.input-player-inputs,
.input-player > div:last-child {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  height: 20%;
}
.input-player-inputs > input {
  cursor: pointer;
  color: black;
  background: beige;
  margin: 0;
  font-size: 1.2rem;
  font-weight: 400;
  padding: 0.48rem 0.96rem;
  border-width: 0;
  border-style: none;
  text-decoration: none;
  outline: none;
}
.input-player-inputs > input::placeholder {
  color: black;
}
.input-player-inputs > input:-ms-input-placeholder {
  color: black;
}
.input-player-inputs > input::-ms-input-placeholder {
  color: black;
}
.input-player-link,
.input-player-inputs > button {
  white-space: nowrap;
  appearance: auto;
  text-rendering: auto;
  color: black;
  background: #3bc565;
  text-shadow: none;
  display: inline-block;
  text-align: center;
  cursor: pointer;
  margin: 0;
  font-size: 1.2rem;
  font-weight: 400;
  padding: 0.48rem 0.96rem;
  border-width: 0;
  border-style: none;
  text-decoration: none;
  outline: none;
}
.input-player-link {
  background: #3bc565;
  font-size: 2rem;
}
.input-player-inputs > div:first-child {
  margin-bottom: 8%;
}

.input-player-list {
  height: 60%;
  overflow-y: auto;

  /* Hide scrollbar for IE, Edge and Firefox */
  -ms-overflow-style: none; /* IE and Edge */
  scrollbar-width: none; /* Firefox */
}
/* Hide scrollbar for Chrome, Safari and Opera */
.input-player-list::-webkit-scrollbar {
  display: none;
}
.input-player-list > h2 {
  font-size: 2rem;
  text-align: center;
  margin: 0.04rem;
}
.input-player-list > p {
  font-size: 1.4rem;
  cursor: pointer;
  text-align: center;
  margin: 0.04rem;
}

input.error::placeholder {
  color: red;
  font-weight: bold;
}
.error:-ms-input-placeholder {
  color: red;
  font-weight: bold;
}
.error::-ms-input-placeholder {
  color: red;
  font-weight: bold;
}
@media only screen and (max-width: 1040px) {
.input-player-inputs > button,
.input-player-inputs > input {
  font-size: 0.8rem;
}
}
@media only screen and (max-width: 600px) {
.input-player-inputs > button,
.input-player-inputs > input {
  font-size: 0.7rem;
}
.input-player-link {
  font-size: 1.2rem;
}
.input-player-list > p {
  font-size: 1.2rem;
  margin: 0;
}
.input-player {
  padding: 0.8rem;
}
.input-player > h2 {
  font-size: 1.4rem;
}
}
</style>