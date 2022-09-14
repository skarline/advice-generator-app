<script setup lang="ts">
import { ref } from "vue"

import axios from "axios"

interface Slip {
  id: number
  advice: string
}

const slip = ref<Slip>({
  id: 117,
  advice:
    "It is easy to sit up and take notice, what's difficult is getting up and taking action."
})

async function fetchAdvice() {
  interface AdviceSlipResponse {
    slip: Slip
  }

  const { data } = await axios.get<AdviceSlipResponse>(
    "https://api.adviceslip.com/advice"
  )

  slip.value = data.slip
}
</script>

<template>
  <div class="card">
    <h5>ADVICE #{{ slip.id }}</h5>
    <q>{{ slip.advice }}</q>
    <img class="divider desktop" src="../assets/pattern-divider-desktop.svg" />
    <img class="divider mobile" src="../assets/pattern-divider-mobile.svg" />
    <button @click="fetchAdvice">
      <img src="../assets/icon-dice.svg" />
    </button>
  </div>
</template>

<style scoped>
.card {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: min-content;
  padding: 48px;
  margin-bottom: 48px;
  box-sizing: border-box;
  border-radius: 16px;
  background-color: hsl(217, 19%, 24%);
  text-align: center;
  box-shadow: 48px 48px 48px hsla(220, 19%, 9%, 0.1);
}
.card > * {
  margin-bottom: 24px;
}
q {
  color: hsl(193, 38%, 86%);
  margin: 0 -2px;
  font-size: 28px;
  font-weight: 800;
}
h5 {
  color: hsl(150, 100%, 66%);
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 4px;
  margin: 0;
}
button {
  position: absolute;
  bottom: -56px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 64px;
  height: 64px;
  border-radius: 32px;
  border: none;
  background-color: hsl(150, 100%, 66%);
  transition: box-shadow 200ms;
  cursor: pointer;
}
button:hover {
  box-shadow: 0 0 16px hsl(150, 100%, 66%);
}
.divider {
  margin-top: 16px;
  margin-bottom: 24px;
}
.divider.mobile {
  display: none;
}
@media (max-width: 768px) {
  .divider.desktop {
    display: none;
  }
  .divider.mobile {
    display: block;
  }
}
</style>
