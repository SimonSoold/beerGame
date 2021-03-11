<template>
    <div class="game-inputbox">
      <input
        v-bind:class="{ error: inputError }"
        v-model="newRuleInput"
        type="text"
        placeholder="Skriv in en regel"
      />
      <a href="#" v-on:click="writeRule()">Skicka</a>
    </div>
</template>

<script>
export default {
    data() { return {
        newRuleInput: "",
        inputError: false,
        }},
    props: {
    }, methods: {
            writeRule() {
      if (this.newRuleInput.length > 9) {
        this.$emit("clicked", this.newRuleInput);
        this.newRuleInput = "";
      } else {
        this.inputError = !this.inputError;
        setTimeout(() => {
          this.inputError = !this.inputError;
        }, 1000);
      }
    }
    }}
</script>

<style>
.game-inputbox > input {
  cursor: pointer;
  color: black;
  margin: 0;
  font-size: 0.8rem;
  font-weight: 400;
  padding: 0.24rem 0.48rem;
  border-style: none;
  text-decoration: none;
  outline: none;
  width: 15vw;
}
.game-inputbox > input::placeholder {
  color: black;
}
.game-inputbox > input:-ms-input-placeholder {
  color: black;
}
.game-inputbox > input::-ms-input-placeholder {
  color: black;
}
.game-inputbox > a {

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
  border: none;
  border-left: 0.08rem solid black;
}
.error {
  box-sizing: border-box;
  color: red;
  border: 4px solid red;
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
.game-inputbox {
  display: flex;
  flex-direction: row;
}
@media only screen and (max-width: 600px) {
.game-inputbox > input {
  width: fit-content;
}
}
</style>