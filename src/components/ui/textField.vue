<template>
  <div class="input-field">
    <div class="input-field__wrapper">
      <label
        v-if="label"
        class="input-field__label"
        :class="{
          'input-field__label--focused': isFocused || input.length > 0,
        }"
        >{{ label }}</label
      >
      <textarea
        v-model="input"
        :cols="cols"
        :rows="rows"
        :maxlength="maxlength"
        @focus="isFocused = true"
        @blur="isFocused = false"
        class="input-field__input"
        :class="{ 'input-field__input--error': isError }"
        :style="{ width: width + 'px', height: height + 'px' }"
      ></textarea>

      <div v-if="isError" class="input-field__error">Ошибка</div>
      <div class="input-field__counter">{{ input.length }}/1000</div>
      <a
        href="javascript:void(0)"
        @click="clearInput"
        class="input-field__clear"
        >Очистить</a
      >
      <div v-if="isLoading" class="input-field__loading"></div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const props = defineProps({
  label: String,
  cols: Number,
  rows: Number,
  maxlength: Number,
  width: Number,
  height: Number,
});

const input = ref("");
const isFocused = ref(false);
const isError = computed(() => input.value.length >= 10);
const isLoading = ref(false);

const clearInput = () => {
  isLoading.value = true;
  setTimeout(() => {
    input.value = "";
    isLoading.value = false;
  }, 1000);
};
</script>

<style scoped lang="scss">
.input-field {
  &__wrapper {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }
  &__label {
    position: absolute;
    top: 10px;
    left: 12px;
    color: #878f97;
    font-size: 11px;
  }
  &__label--focused {
    transform: translateY(-8px);
    transition: transform 0.3s ease;
  }
  &__input {
    color: #4f4f4f;
    background-color: #f0f0f0;
    border-radius: 10px;
    font-size: 16px;
    padding: 12px 12px;
    &:focus {
      cursor: pointer;
      outline: none;
    }
    &--error {
      background-color: #fbf0ef;
    }
  }
  &__counter {
    color: #878f97;
  }
  &__error {
    color: #d6675c;
  }
  &__clear {
    color: #00b6d0;
  }
  &__loading {
    position: absolute;
    top: 10px;
    right: 10px;
    display: inline-block;
    width: 20px;
    height: 20px;
    border: 2px solid #f3f3f3;
    border-radius: 50%;
    border-top: 2px solid #3498db;
    animation: spin 2s linear infinite;
  }
  .input-field__error,
  .input-field__counter,
  .input-field__clear {
    align-self: flex-start;
  }

  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
}
</style>
