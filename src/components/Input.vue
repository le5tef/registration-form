<template>
  <div class="user-details">
    <div class="input-box">
      <span class="label">{{ inputBox.name }}</span>
      <input
        @input="$emit('input', $event.target.value)"
        :value="value"
        type="text"
        :placeholder="inputBox.placeholder"
      />
      <span v-show="!valid && isDataChecked" class="incorrectData"
        >Введено не корректное значение</span
      >
    </div>
  </div>
</template>
            
<script>
export default {
  props: {
    inputBox: {
      type: Object,
    },
    valid: {
      type: Boolean,
    },
    isDataChecked: {
      type: Boolean,
    },
    value: {
      type: String,
    },
  },
};
</script>
            
<style>
.input-box input {
  height: 52px;
  border: 1px solid #dbe2ea;
  outline: none;
  border-radius: 6px;
  padding: 1px 1px 1px 16px;
  font-size: 16px;
  border-color: #dbe2ea;
}
.user-details,
.input-box {
  display: flex;
  flex-direction: column;
  position: relative;
}
.input-box input::placeholder {
  color: #7c9cbf;
  font-size: 16px;
}
.input-box input:focus {
  border: 2px solid #0880ae;
  padding: 0 0px 0px 15px;
}
.input-box .label {
  margin-top: 30px;
  color: #756f86;
  margin-bottom: 7px;
}
.incorrectData {
  display: block;
  font-size: 14px;
  font-weight: 400;
  color: #ff7171;
}
</style>