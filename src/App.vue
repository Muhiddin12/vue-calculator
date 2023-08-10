<template>
  <div class="calculator">
    <div class="view">
      <input type="text" ref="display" class="display" />
    </div>
    <table @click="table">
      <tr>
        <td class="blackColor clearColor">C</td>
        <td class="back blackColor">Back</td>
        <td class="blackColor">+/-</td>
        <td class="gold">%</td>
      </tr>
      <tr>
        <td class="number">7</td>
        <td class="number">8</td>
        <td class="number">9</td>
        <td class="gold">*</td>
      </tr>
      <tr>
        <td class="number">4</td>
        <td class="number">5</td>
        <td class="number">6</td>
        <td class="gold">/</td>
      </tr>
      <tr>
        <td class="number">1</td>
        <td class="number">2</td>
        <td class="number">3</td>
        <td class="gold">-</td>
      </tr>
      <tr>
        <td class="number zero">0</td>
        <td class="number">.</td>
        <td class="number">=</td>
        <td class="gold plus">+</td>
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
      if (character == "C") {
        this.$refs.display.value = "";
      } else if (character == "=") {
        this.$refs.display.value = eval(this.$refs.display.value);
      } else if (character == "Back") {
        this.$refs.display.value = this.$refs.display.value.slice(
          0,
          this.$refs.display.value.length - 1
        );
      } else if (character == "+/-") {
        console.log("ok");
        this.$refs.display.value = "(-" + this.$refs.display.value;
      } else {
        this.$refs.display.value += character;
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
.calculator {
  max-width: 320px;
  margin-top: 90px;
  border-radius: 18px;
  margin: 90px auto;
}
.display {
  width: 100%;
  height: 100px;
  box-sizing: border-box;
  caret-color: white;
  font-size: 60px;
  border-radius: 18px 18px 0 0;
  padding: 0 14px;
  text-align: right;
  background: #151515;
  color: white;
  font-size: 40px;
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
  height: 70px;
  font-size: 35px;
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
.back {
  font-size: 25px;
  font-weight: 300;
}
.plus {
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

