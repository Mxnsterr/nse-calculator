<template>
  <div id="app">
    <main>
      <div class="company">
        <img class="logo" src="./assets/nse.png" />
        <p class="name">NSE Surcharge Calculator</p>
      </div>
      <form @submit.prevent="submit">
        <div class="inputs">
            <input 
              type="number" 
              class="input-kms"
              placeholder="Amount of kms" 
              v-model="kms"
              min="0" 
              max="540"
              step="0.01"
              />
            <input 
              type="number" 
              class="input-surcharge"
              placeholder="Fuel surcharge %" 
              v-model="fuelsurcharge"
              min="-100" 
              max="100"
              step="0.01"
              />
        <button class="submit" type="submit">
            Calculate surcharge <fa class='icon-calc' icon="circle-arrow-right"/>
        </button>
        </div>
      </form>

      <div class="final-box">
        <div class="results-p">Calculated Results</div>
        <div class="kms-output">Amount of kms: {{ kms }} kms</div>
        <div class="surcharge-output">Surcharge per month: {{ fuelsurcharge }}%</div>
        <div class="price-output">Rate including 1 stop: €{{ price }}</div>
        <div class="surcharge-output-calc">Result fuel surcharge: €{{ surcharge }}</div>
        <div class="final-output"><stong>Total: €{{ final }}</stong></div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      kms: '',
      fuelsurcharge: '',
      final: '',
      price: ''
    }
  },
  methods: {
    submit() {
      if (this.kms < 0 || this.kms > 540) {
          this.final = 'Invalid value'
      }
      else {
        var value = 0
        switch (true) {
          case (this.kms >= 0 && this.kms <= 20):
            value = 250
            break;
          case (this.kms >= 21 && this.kms <= 40):
            value = 275
            break;
          case (this.kms >= 41 && this.kms <= 60):
            value = 305
            break;
          case (this.kms >= 61 && this.kms <= 120):
            value = 330
            break;
          case (this.kms >= 121 && this.kms <= 160):
            value = 360
            break;
          case (this.kms >= 161 && this.kms <= 200):
            value = 385
            break;
          case (this.kms >= 201 && this.kms <= 260):
            value = 425
            break;
          case (this.kms >= 261 && this.kms <= 320):
            value = 465
            break;
          case (this.kms >= 321 && this.kms <= 380):
            value = 495
            break;
          case (this.kms >= 381 && this.kms <= 400):
            value = 530
            break;
          case (this.kms >= 401 && this.kms <= 440):
            value = 550
            break;
          case (this.kms >= 441 && this.kms <= 460):
            value = 580
            break;
          case (this.kms >= 461 && this.kms <= 480):
            value = 605
            break;
          case (this.kms >= 481 && this.kms <= 500):
            value = 640
            break;
          case (this.kms >= 501 && this.kms <= 520):
            value = 660
            break;
          case (this.kms >= 521 && this.kms <= 540):
            value = 690
            break;
        }
        this.price = value
        this.surcharge = Math.round((value / 100 * this.fuelsurcharge) * 100) / 100
        this.final = this.surcharge + this.price
      }
    }
  }
}
</script>

<style>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('./assets/background.jpeg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.35), rgba(0,0,0,0.75));
}

.company {
  display: flex;
  flex-direction: row;
  align-content: center;
  justify-content: left;
  align-items: center;
  background: rgba(255, 255, 255, 0.75);
  width: auto;
  border-left: 5px solid #f7960f;
  margin: 5vh;
}

.logo {
  width: 20vh;
  height: auto;
}

.name {
  color: #144A62;
  font-size: 75px;
}

.inputs {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-evenly;
}

::placeholder {
  color: #144A62;
  opacity: 0.5;
}

.input-kms {
  width: 25%;
  display: block;
  padding: 35px;
  font-weight: 700;
  text-shadow: 1.5px 1.5px rgba(0, 0, 0, 0.5);
  text-align: center;
  outline: none;
  background: rgba(255, 255, 255, 0.75);
  color: #144A62;
  border-left: 5px solid #f7960f;
  border-right: none;
  border-top: none;
  border-bottom: none;
}

.input-kms:focus {
  box-shadow: 0px 0px 16px rgba(43, 43, 43, 0.25);
  background: rgba(255, 255, 255, 0.85);
}

.input-surcharge {
  display: block;
  width: 25%;
  padding: 35px;
  font-weight: 700;
  text-shadow: 1.5px 1.5px rgba(0, 0, 0, 0.5);
  text-align: center;
  outline: none;
  background: rgba(255, 255, 255, 0.75);
  transition: 0.4s;
  color: #144A62;
  border-left: 5px solid #f7960f;
  border-right: none;
  border-top: none;
  border-bottom: none;
}

.input-surcharge:focus {
  box-shadow: 0px 0px 16px rgba(43, 43, 43, 0.25);
  background: rgba(255, 255, 255, 0.85);
}

.location-box .location {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.final-box {
  background: rgba(255, 255, 255, 0.75);
  font-size: 40px;
  color: #313131;
  padding: 5vh;
  margin-top: 5vh;
  margin-left: 12vh;
  display: flex;
  flex-direction: column;
  width: 88%;
  border-left: 5px solid #f7960f;
}

.final-box .results-p {
  display: inline-block;
  color: #144A62;
  font-size: 60px;
  padding-bottom: 2vh;
}

.final-box .kms-output {
  display: inline-block;
  color: #144A62;
}

.final-box .surcharge-output {
  display: inline-block;
  color: #144A62;
}

.final-box .price-output {
  display: inline-block;
  color: #144A62;
}

.final-box .surcharge-output-calc {
  display: inline-block;
  color: #144A62;
}

.final-box .final-output {
  display: inline-block;
  color: #144A62;
  font-size: 50px;
  padding-top: 2vh;
}

.submit {
  width: 25%;
  display: block;
  padding: 35px;
  font-size: 50px;
  font-weight: 700;
  text-shadow: 1.5px 1.5px rgba(0, 0, 0, 0.5);
  text-align: center;
  outline: none;
  background: rgba(255, 255, 255, 0.75);
  color: #144A62;
  border-left: 5px solid #f7960f;
  border-right: none;
  border-top: none;
  border-bottom: none;
  transition: 0.4s;
}

.submit:hover {
  background-color: rgba(255, 255, 255, 0.95);
  transition: 0.4s;
}

.icon-calc {
  font-size: 35px;
  color: #f7960f;
}

@media screen and (min-width: 2540px) {
    .submit {
      font-size: 50px;
    }
    .input-kms { 
      font-size: 50px;
    }
    .input-surcharge { 
      font-size: 50px;
    }
    .final-box {
      margin-left: 12vh;
      width: 88%;
    }
}

@media screen and (max-width: 2539px) {
    .submit {
      font-size: 30px;
    }
     .input-kms { 
      font-size: 30px;
    }
    .input-surcharge { 
      font-size: 30px;
    }
    .final-box {
      margin-left: 11vh;
      width: 87.5%;
    }
}

</style>
