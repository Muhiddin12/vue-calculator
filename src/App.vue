<template>
  <div class="calculator">
    <div class="ui">
      <div class="view">
        <div class="display" ref="display"></div>
      </div>
    </div>
    <table @click="table">
      <tr>
        <td class="blackColor clearColor">C</td>
        <td class="back blackColor">Back</td>
        <td class="blackColor">%</td>
        <td class="gold">*</td>
      </tr>
      <tr>
        <td class="number">7</td>
        <td class="number">8</td>
        <td class="number">9</td>
        <td class="gold">/</td>
      </tr>
      <tr>
        <td class="number">4</td>
        <td class="number">5</td>
        <td class="number">6</td>
        <td class="gold">-</td>
      </tr>
      <tr>
        <td class="number">1</td>
        <td class="number">2</td>
        <td class="number">3</td>
        <td class="gold">+</td>
      </tr>
      <tr>
        <td class="number zero">0</td>
        <td class="number">00</td>
        <td class="number">.</td>
        <td class="gold right">=</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "App",
  methods: {
    table(event) {
      let character = event.target.closest("td").innerText;
      let fullWord = this.$refs.display.innerText;
      let lastWord = fullWord.slice(fullWord.length - 1, fullWord.length);
      console.log(character);
      console.log(lastWord);

      if (character == "=" && fullWord.includes("%")) {
        let protsentIndex = fullWord.indexOf("%");
        let beforeProtsent = fullWord.slice(0, protsentIndex);
        let afterProtsent = fullWord.slice(protsentIndex + 1, fullWord.length);
        this.$refs.display.innerText = (beforeProtsent * afterProtsent) / 100;
        // alert(beforeProtsent);
        // alert(afterProtsent);
      } else if (character == "C") {
        this.$refs.display.innerText = "";
      } else if (character == "=" && this.$refs.display.innerText == "") {
        alert("Xato !");
      } else if (character == "=") {
        this.$refs.display.innerText = eval(this.$refs.display.innerText);
      } else if (character == "Back") {
        this.$refs.display.innerText = this.$refs.display.innerText.slice(
          0,
          this.$refs.display.innerText.length - 1
        );
      } else if (character == "+/-") {
        console.log("ok");
        this.$refs.display.innerText = "(-" + this.$refs.display.innerText;
      } else if (
        character == lastWord &&
        character != 1 &&
        character != 2 &&
        character != 3 &&
        character != 4 &&
        character != 5 &&
        character != 6 &&
        character != 7 &&
        character != 8 &&
        character != 9 &&
        character != 0
      ) {
        alert("Xato !");
        this.$refs.display.innerText = "";
      } else if (
        (character == "*" || character == "/") &&
        (lastWord == "%" || character == "-")
      ) {
        alert("!Number");
      } else {
        this.$refs.display.innerText += character;
      }
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body {
  background: #333333;
}
.ui {
  width: 310px;
  background: #131313;
  border-radius: 18px 18px 0 0;
}
.calculator {
  max-width: 310px;
  margin-top: 90px;
  border-radius: 18px;
  margin: 90px auto;
}
.view {
  margin: 0 10px;
  padding: 0;
  height: 100px;
  overflow-x: auto;
  width: 290px;
  display: flex;
}
.view::-webkit-scrollbar {
  width: 0;
}
.display {
  margin: 30px 12px;
  width: 290px;
  box-sizing: border-box;
  caret-color: white;
  font-size: 60px;
  text-align: right;
  color: white;
  font-size: 40px;
  border: none;
}
table {
  width: 100%;
  color: white;
  font-weight: bold;
  font-size: 40px;
  height: 80%;
}
td {
  text-align: center;
  width: 25%;
  height: 60px;
  font-size: 30px;
}
.blackColor {
  background: #4a4a4a;
  font-size: 30px;
}
.gold {
  background: rgb(205, 175, 1);
  font-size: 30px;
}
.number {
  background: rgba(129, 129, 129, 0.812);
}
td:hover {
  background-color: rgb(255, 255, 255);
  color: black;
  cursor: pointer;
  transition: 0.6s;
}
td:active {
  font-size: 22px;
  transition: 0.6s;
}
.back {
  font-size: 25px;
  font-weight: 300;
}
.right {
  border-radius: 0 0 18px 0;
}
.zero {
  border-radius: 0 0 0 18px;
}
.clearColor {
  font-size: 30px;
  font-weight: 300;
}
</style>
