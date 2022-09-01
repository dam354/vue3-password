<script setup>
  import { ref } from "vue";
  import FieldPassword from "./components/fieldPassword.vue";
  import FieldSettings from "./components/FieldSettings.vue";

  const alphaUpper = ref("ABCDEFGHIJKLMNOPQRSTUVWXYZ");
  const alphaLower = ref("abcdefghijklmnopqrstuvwxyz");
  const numbers = ref("0123456789");
  const symbols = ref("!@#$%^&*_-+=");

  const Password = ref("");
  const inputCharCount = ref(10);
  const inputUpper = ref(true);
  const inputLower = ref(true);
  const inputNumber = ref(true);
  const inputSymbols = ref(false);

  const generatedPassword = () => {
    let possibleCharacters = "";

    inputUpper.value ? (possibleCharacters += alphaUpper.value) : "";
    inputLower.value ? (possibleCharacters += alphaLower.value) : "";
    inputNumber.value ? (possibleCharacters += numbers.value) : "";
    inputSymbols.value ? (possibleCharacters += symbols.value) : "";

    let tempPassword = "";
    for (let i = 0; i < inputCharCount.value; i++) {
      tempPassword += possibleCharacters.charAt(Math.floor(Math.random() * possibleCharacters.length));
    }
    Password.value = tempPassword;
  };
</script>

<template>
  <div class="flex justify-center align-middle h-screen w-full">
    <div class="flex flex-col justify-center align-middle max-w-xl w-full mx-5">
      <h1 class="mx-auto mb-5 text-lg" style="color: hsl(var(--grayMed))">Vue 3 Password Generator</h1>

      <FieldPassword :password="Password" />
      <FieldSettings
        v-model:inputCharCount="inputCharCount"
        v-model:inputUpper="inputUpper"
        v-model:inputLower="inputLower"
        v-model:inputNumber="inputNumber"
        v-model:inputSymbols="inputSymbols"
        v-model:generatedPassword="generatedPassword"
      />
    </div>
  </div>
</template>

<style></style>
