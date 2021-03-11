<template>
<div class="deck">
    <p v-on:click="write()">skriv</p>
</div>
</template>

<script>
export default {
    name: 'Deck',
    data() {return {
        Deck: []
    }},
    methods: {
        Shuffle() {
            let types = ["clubs", "spade", "diamond", "heart"]
            for (let i = 0; i < 13; i++) {
                for (let current of types) {
                    this.Deck.push({'value': this.checkValue(i+2), 'type': current, 'color': this.checkColor(current), 'src': 'clubs.png'})
                }
            }
        }, checkColor(type) {
            if (type === "clubs" || type === "spade") {
                return "black"
            } else {
                return "red"
            }
        }, checkValue(value) {
            switch (Number(value)) {
                case 11: return "kn"
                case 12: return "D"
                case 13: return "K"
                case 14: return "E"
                default: return value
            }
        }, write() {
    const data = JSON.stringify(this.Deck)
    const blob = new Blob([data], {type: 'text/plain'})
    const e = document.createEvent('MouseEvents'),
    a = document.createElement('a');
    a.download = "test.json";
    a.href = window.URL.createObjectURL(blob);
    a.dataset.downloadurl = ['text/json', a.download, a.href].join(':');
    e.initEvent('click', true, false, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);
    a.dispatchEvent(e);
    }
    }, created() {
        this.Shuffle()
    } 
}
</script>

<style>
.deck {
    height: 100%;
    width: 100%;
    box-sizing: border-box;
    padding: 2.4rem;
    background: white;
    border-radius: 5%;
}
</style>