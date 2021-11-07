<template>
  <div class="container">
    <div class="title">Регистрация</div>
    <div class="subtitle">
      Уже есть аккаунт?<a href="#" class="link-button">Войти</a>
    </div>
    <form @submit.prevent="checkData()">
      <div class="user-details">
        <Input />
        <div class="input-box">
          <span class="details">Email</span>
          <input v-model="email" type="text" placeholder="Введите ваш Email" />
          <span v-show="!validEmail && isDataChecked" class="incorrectData"
            >Введено не корректное значение</span
          >
        </div>
        <div class="input-box">
          <span class="details">Номер телефона</span>

          <input
            v-model="phone"
            type="text"
            placeholder="Введите номер телефона"
          />
          <span v-show="!validEmail && isDataChecked" class="incorrectData"
            >Введено не корректное значение</span
          >
        </div>
      </div>
      <div class="dropdown">
        <div class="select" @click="showDropDownList = !showDropDownList">
          <span :class="language ? '' : 'placeholder-color'">{{
            language ? languages[language] : "Язык"
          }}</span>

          <svg style="width: 30px; height: 30px" viewBox="0 0 24 24">
            <path
              fill="#0880AE"
              d="M7.41,8.58L12,13.17L16.59,8.58L18,10L12,16L6,10L7.41,8.58Z"
            />
          </svg>
        </div>

        <div v-show="showDropDownList" class="dropdown-list">
          <div
            v-for="(lang, key) in languages"
            :key="key"
            @click="selectLanguage(key)"
            class="dropdown-list-item"
            :class="{ 'active-lang': language == key }"
          >
            {{ lang }}
          </div>
        </div>
      </div>
      <span v-show="!language && isDataChecked" class="incorrectData"
        >Введено не корректное значение</span
      >
      <div>
        <div class="check-box">
          <input
            type="checkbox"
            id="id_agree"
            v-model="acceptTerms"
            class="hidden"
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
      <div class="button">
        <input
          :class="acceptTerms ? 'active' : 'disabled'"
          :disabled="!acceptTerms"
          type="submit"
          value="Зарегистрироваться"
        />
      </div>
    </form>
  </div>
</template>
<script>
import Input from "./Input.vue";

export default {
  components: {
    Input,
  },
  data() {
    return {
      showDropDownList: false,
      isDataChecked: false,
      name: "",
      email: "",
      phone: "",
      language: "",
      validName: false,
      validEmail: false,
      validPhone: false,
      languages: {
        ru: "Русский",
        en: "Английский",
        ch: "Китайский",
        sp: "Испанский",
      },
      inputBoxes: [
        {
          name: "Имя",
          placeholder: "Введите Ваше Имя",
        },
      ],
      acceptTerms: false,
    };
  },
  methods: {
    selectLanguage(id) {
      this.language = id;
      this.showDropDownList = false;
    },
    acceptTheTerms() {
      this.acceptTerms = !this.acceptTerms;
    },
    checkData() {
      var regExName =
        /^[A-ZА-Я]{1}[a-zа-я]{3,14}( [A-ZА-Я]{1})?([a-zа-я]{3,14})?(-[A-ZА-Я]{1})?([a-zа-я]{3,14})?$/;
      var regExEmail =
        /^(?!.*@.*@.*$)(?!.*@.*--.*\..*$)(?!.*@.*-\..*$)(?!.*@.*-$)(.*@.+(\..{1,11})?)$/;
      var regExPhone = /\(?([0-9]{3})\)?([ .-]?)([0-9]{3})\2([0-9]{4})/;
      this.validName = regExName.test(this.name);
      this.validEmail = regExEmail.test(this.email);
      this.validPhone = regExPhone.test(this.phone);
      this.isDataChecked = true;
    },
  },
};
</script>
<style scoped>
.container {
  margin: 0 auto;
  background-color: white;
  min-width: 300px;
  max-width: 400px;
  padding: 40px 30px;
  border-radius: 20px;
}
.container .title {
  font-size: 34px;
  font-weight: 700;
}
.container .subtitle,
details {
  font-size: 16px;
  font-weight: 400;
}
.subtitle .link-button {
  margin-left: 6px;
}
.container .subtitle {
  margin-bottom: 20px;
}
.container .details,
.check-box {
  color: #756f86;
}
.container .details {
  margin-bottom: 7px;
}
.container .check-box .label {
  margin-bottom: 40px;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.container .check-box .button {
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
.check-box {
  margin-top: 30px;
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

.container form .user-details,
.input-box {
  display: flex;
  flex-direction: column;
  position: relative;
}
.container .link-button {
  border: none;
  background: none;
  text-decoration: none;
  color: #0880ae;
  font-size: 16px;
  padding: 0;
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
.placeholder-color {
  color: #7c9cbf;
}

.dropdown .active {
  opacity: 1;
  visibility: visible;
}
.dropdown:hover .select {
  border: 2px solid #0880ae;
  padding: 15px;
}
.dropdown-list {
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
.dropdown-list-item {
  padding: 16px;
  cursor: pointer;
}
.active-lang,
.dropdown-list-item:hover {
  background-color: #ebf4f8;
}
.user-details .input-box input {
  height: 52px;
  border: 1px solid #dbe2ea;
  outline: none;
  border-radius: 6px;

  padding: 1px 1px 1px 16px;
  font-size: 16px;
  border-color: #dbe2ea;
}
.user-details .input-box input::placeholder {
  color: #7c9cbf;
  font-size: 16px;
}
.user-details .input-box input:focus {
  border: 2px solid #0880ae;
  padding: 0 0px 0px 15px;
}
.user-details .input-box .details {
  margin-top: 30px;
}
form .button {
  height: 56px;
}
form .button input {
  height: 100%;
  width: 100%;
  outline: none;
  border: none;
  font-size: 16px;
}
.button .active {
  border-radius: 6px;
  background-color: #0880ae;
  color: #ebf4f8;
  cursor: pointer;
}
.button .disabled {
  color: #b1b5bf;
  background-color: #dbe2ea;
  border-radius: 6px;
}
.hidden {
  display: none;
}
.incorrectData {
  display: block;
  font-size: 14px;
  font-weight: 400;
  color: #ff7171;
}
</style>