<script setup>
  import { ref, toRef, computed } from "vue";

  const props = defineProps({
    inputCharCount: String,
    inputUpper: Boolean,
    inputLower: Boolean,
    inputNumber: Boolean,
    inputSymbols: Boolean,
    generatedPassword: Function,
  });

  const sliderPercent = computed(() => {
    return (parseInt(props.inputCharCount) / 20) * 100 + "%";
  });
</script>

<template>
  <div class="settings-container">
    <div class="mb-8">
      <div class="flex justify-between items-center mb-4">
        <label class="block" for="inputCharCount">Character Length </label>
        <h3 class="charCount">{{ inputCharCount }}</h3>
      </div>
      <input type="range" id="inputCharCount" min="1" max="20" v-model="inputCharCount" @input="$emit('update:inputCharCount', $event.target.value)" />
    </div>
    <div class="mb-5 flex">
      <input type="checkbox" id="inputUpper" v-model="inputUpper" @change="$emit('update:inputUpper', $event.target.checked)" />
      <label for="inputUpper">Include Uppercase Letters</label>
    </div>
    <div class="mb-5 flex">
      <input type="checkbox" id="inputLower" v-model="inputLower" @change="$emit('update:inputLower', $event.target.checked)" />
      <label for="inputLower">Include Lowercase Letters</label>
    </div>
    <div class="mb-5 flex">
      <input type="checkbox" id="inputNumber" v-model="inputNumber" @change="$emit('update:inputNumber', $event.target.checked)" />
      <label for="inputNumber">Include Numbers</label>
    </div>
    <div class="mb-5 flex">
      <input type="checkbox" id="inputSymbols" v-model="inputSymbols" @change="$emit('update:inputSymbols', $event.target.checked)" />
      <label for="inputSymbols">Include Symbols</label>
    </div>
    <button class="generate group" @click="generatedPassword">
      Generate
      <svg width="12" class="generateArrow" height="12" xmlns="http://www.w3.org/2000/svg"><path fill="#24232C" d="m5.106 12 6-6-6-6-1.265 1.265 3.841 3.84H.001v1.79h7.681l-3.841 3.84z" /></svg>
    </button>
  </div>
</template>

<style>
  .generate {
    /* border: 2px solid hsl(var(--green)); */
    background-color: hsl(var(--green));
    color: hsl(var(--grayDark));
    width: 100%;
    padding: 18px 0;
    display: flex;
    justify-content: center;
    align-items: center;
    border: 2px solid hsl(var(--grayDark));

    @apply ease-out duration-100;
  }
  .generateArrow {
    margin-left: 24px;
    @apply ease-out duration-100;
  }
  .generate:hover .generateArrow {
    transform: translateX(4px);
  }
  .generate:active {
    background-color: hsl(var(--grayDark));
    color: hsl(var(--green));
    border: 2px solid hsl(var(--green));
  }
  .generate:active .generateArrow path {
    fill: hsl(var(--green)) !important;
  }

  .settings-container {
    width: 100%;

    background-color: hsl(var(--grayDark));

    padding: 28px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .charCount {
    color: hsl(var(--green));
  }

  /*********** Baseline, reset styles ***********/
  input[type="range"] {
    -webkit-appearance: none;
    appearance: none;
    background: transparent;
    cursor: pointer;
    width: 100%;
  }

  /* Removes default focus */
  input[type="range"]:focus {
    outline: none;
    outline: none;
  }

  /******** Chrome, Safari, Opera and Edge Chromium styles ********/
  /* slider track */
  input[type="range"]::-webkit-slider-runnable-track {
    background: linear-gradient(to right, hsl(var(--green)) 0%, hsl(var(--green)) v-bind(sliderPercent), hsl(var(--black)) v-bind(sliderPercent), hsl(var(--black)) 100%);
    border-radius: 0rem;
    height: 8px;
  }

  /* slider thumb */
  input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none; /* Override default look */
    appearance: none;
    margin-top: -10px; /* Centers thumb on the track */
    background-color: hsl(var(--grayLight));
    outline: 3px solid hsl(var(--grayLight));
    border-radius: 50%;
    height: 28px;
    width: 28px;
  }

  input[type="range"]:focus::-webkit-slider-thumb,
  input[type="range"]:hover::-webkit-slider-thumb {
    outline: 3px solid hsl(var(--green));
    background-color: hsl(var(--black));
    @apply ease-out duration-300;
  }

  /*********** Firefox styles ***********/
  /* slider track */
  input[type="range"]::-moz-range-track {
    background-color: #59ff00;
    border-radius: 0rem;
    height: 8px;
  }

  /* slider thumb */
  input[type="range"]::-moz-range-thumb {
    background-color: hsl(var(--grayLight));
    outline: 3px solid hsl(var(--grayLight));
    border: none; /*Removes extra border that FF applies*/
    border-radius: 50%;
    height: 25px;
    width: 25px;
  }

  input[type="range"]:focus::-moz-range-thumb,
  input[type="range"]:hover::-moz-range-thumb {
    outline: 3px solid hsl(var(--green));
    background-color: hsl(var(--black));
    @apply ease-out duration-100;
  }
</style>
