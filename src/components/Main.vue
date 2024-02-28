<template>
  <div class="container">
    <h4>Текст перед полем ввода</h4>
    <textField
      label="Название поля"
      cols="30"
      rows="10"
      maxlength="500"
      width="326px"
      height="146px"
    />
  </div>
</template>

<script setup>
import textField from "@/components/ui/textField.vue";
</script>
<style lang="scss">
.container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  height: 100vh;
  margin-left: 20%;
}
h4 {
  padding: 8px;
  font-size: 18px;
  font-weight: 500;
  line-height: 24px;
  letter-spacing: 0.0015em;
  text-align: left;
  margin-bottom: 0px;
}
</style>
