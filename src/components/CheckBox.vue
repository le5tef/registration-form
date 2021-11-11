<template>
  <div>
    <div class="check-box">
      <input
        type="checkbox"
        id="id_agree"
        v-model="acceptTerms"
        class="hidden"
        @input="$emit('input', $event.target.value)"
      />
      <label class="text label" for="id_agree">
        <div
          id="acceptTermsButton"
          :class="acceptTerms ? 'active-check-box' : ''"
          class="button"
        >
          <svg
            v-show="acceptTerms"
            style="width: 24px; height: 24px"
            viewBox="0 0 24 24"
          >
            <path
              fill="#0880AE"
              d="M21,7L9,19L3.5,13.5L4.91,12.09L9,16.17L19.59,5.59L21,7Z"
            />
          </svg>
        </div>
        &nbsp;Принимаю&nbsp;
        <a class="link-button" href="#">условия </a>&nbsp;использования
      </label>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      acceptTerms: false,
    };
  },
};
</script>

<style scoped>
.hidden {
  display: none;
}

.check-box {
  color: #756f86;
  margin-top: 30px;
}
.link-button {
  border: none;
  background: none;
  text-decoration: none;
  color: #0880ae;
  font-size: 16px;
  padding: 0;
}
.check-box .label {
  margin-bottom: 40px;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.check-box .button {
  position: relative;
  height: 28px;
  width: 28px;
  border-radius: 4px;
  border: 1px solid #dbe2ea;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.check-box .text {
  margin-left: 8px;
}
.active-check-box::before {
  content: "";
  border-radius: 4px;
  position: absolute;
  height: 28px;
  width: 28px;
  border: 2px solid #0880ae !important;
}
</style>