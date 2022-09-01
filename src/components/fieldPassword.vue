<script setup>
  import { ref } from "vue";

  const props = defineProps({
    password: String,
  });

  const copiedTimer = ref(false);

  const copyToClipboard = async () => {
    try {
      await navigator.clipboard.writeText(props.password);
      copiedTimer.value = true;
      setTimeout(() => {
        copiedTimer.value = false;
      }, 2000);
    } catch (err) {
      console.error("Failed to copy!", err);
    }
  };
</script>

<template>
  <div class="password-container mb-7">
    <div class="password-field">
      <h2 v-if="password">{{ password }}</h2>
      <h2 v-else class="placeholder">test</h2>
    </div>
    <button v-if="props.password" class="password-copy" :class="copiedTimer ? 'before:opacity-100' : 'before:opacity-0'" @click="copyToClipboard">
      <img src="/src/assets/img/icon-copy.svg" alt="" />
    </button>
  </div>
</template>

<style scoped>
  .password-container {
    height: 80px;
    width: 100%;

    background-color: hsl(var(--grayDark));

    padding: 0 28px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .password-copy {
    position: relative;
  }
  .password-copy img {
    @apply ease-out duration-300;
  }
  .password-copy:hover img {
    filter: brightness(0) invert(1);
  }
  .password-copy::before {
    content: "Copied";
    position: absolute;
    color: hsl(var(--green));
    right: 150%;

    @apply ease-out duration-300;
  }

  .placeholder {
    color: hsl(var(--grayMed));
  }
</style>
