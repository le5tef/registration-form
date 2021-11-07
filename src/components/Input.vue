<template>
  <div class="input-box">
    <span class="details">{{}}</span>
    <input v-model="name" type="text" placeholder="Введите Ваше Имя" />
    <span v-show="!validName && isDataChecked" class="incorrectData"
      >Введено не корректное значение</span
    >
  </div>
</template>
            
<script>
export default {
  props: {
    inputBoxType: {
      type: Object,
    },
  },
};
</script>
            
<style>
</style>