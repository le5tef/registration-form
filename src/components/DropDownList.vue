<template>
  <div>
    <div class="dropdown">
      <div
        class="select"
        :class="showDropDownList ? 'focus' : ''"
        @click="showDropDownList = !showDropDownList"
      >
        <span :class="selectedLanguage ? '' : 'placeholder-color'">{{
          selectedLanguage ? languages[selectedLanguage] : "Язык"
        }}</span>

        <svg style="width: 30px; height: 30px" viewBox="0 0 24 24">
          <path
            fill="#0880AE"
            d="M7.41,8.58L12,13.17L16.59,8.58L18,10L12,16L6,10L7.41,8.58Z"
          />
        </svg>
      </div>

      <div v-show="showDropDownList" class="list">
        <div
          v-for="(lang, key) in languages"
          :key="key"
          @click="selectLanguage(key)"
          class="item"
          :class="{ 'active-lang': selectedLanguage == key }"
        >
          {{ lang }}
        </div>
      </div>
    </div>
    <span v-show="!selectedLanguage && isDataChecked" class="incorrectData"
      >Введено не корректное значение</span
    >
  </div>
</template>

<script>
export default {
  props: {
    languages: {
      type: Object,
    },
    isDataChecked: {
      type: Boolean,
    },
  },
  data() {
    return {
      selectedLanguage: "",
      showDropDownList: false,
    };
  },
  methods: {
    selectLanguage(id) {
      this.selectedLanguage = id;
      this.showDropDownList = false;
    },
  },
};
</script>

<style scoped>
.dropdown .active {
  opacity: 1;
  visibility: visible;
}
.dropdown .focus {
  border: 2px solid #0880ae;
  padding: 15px;
}
.dropdown .list {
  border-radius: 6px;
  background-color: white;
  border: 1px solid #dbe2ea;
  color: #756f86;
  position: absolute;
  z-index: 2;
  top: 110%;
  left: 0;
  right: 0;
  transition: 0.2s;
}
.dropdown .list .item {
  padding: 16px;
  cursor: pointer;
}
.active-lang,
.dropdown .list .item:hover {
  background-color: #ebf4f8;
}
.dropdown {
  margin-top: 30px;
  width: 100%;
  position: relative;
}

.dropdown .select {
  padding: 16px 16px 16px 16px;
  border-radius: 6px;

  background-clip: white;
  border: 1px solid #dbe2ea;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>