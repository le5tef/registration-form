<template>
  <div class="container">
    <div class="title">Регистрация</div>
    <div class="subtitle">
      Уже есть аккаунт?<a href="#" class="link-button">Войти</a>
    </div>
    <form @submit.prevent="checkData()">
      <Input
        :inputBox="inputBoxes[0]"
        :valid="validName"
        v-model="name"
        :isDataChecked="isDataChecked"
      />
      <Input
        :inputBox="inputBoxes[1]"
        :valid="validEmail"
        v-model="email"
        :isDataChecked="isDataChecked"
      />
      <Input
        :inputBox="inputBoxes[2]"
        :valid="validPhone"
        v-model="phone"
        :isDataChecked="isDataChecked"
      />

      <DropDownList :languages="languages" :isDataChecked="isDataChecked" />
      <CheckBox v-model="acceptTerms" />
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
import CheckBox from "./CheckBox.vue";
import DropDownList from "./DropDownList.vue";
import Input from "./Input.vue";

export default {
  components: {
    Input,
    DropDownList,
    CheckBox,
  },
  data() {
    return {
      name: "",
      phone: "",
      email: "",
      acceptTerms: false,
      isDataChecked: false,
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
        {
          name: "Email",
          placeholder: "Введите Ваш Email",
        },
        {
          name: "Номер телефона",
          placeholder: "Введите номер телефона",
        },
      ],
    };
  },
  computed: {
    // ...mapState({ valid }),
  },
  methods: {
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

.container .link-button {
  border: none;
  background: none;
  text-decoration: none;
  color: #0880ae;
  font-size: 16px;
  padding: 0;
}

.placeholder-color {
  color: #7c9cbf;
}

.input-box input {
  height: 52px;
  border: 1px solid #dbe2ea;
  outline: none;
  border-radius: 6px;

  padding: 1px 1px 1px 16px;
  font-size: 16px;
  border-color: #dbe2ea;
}
.input-box input::placeholder {
  color: #7c9cbf;
  font-size: 16px;
}
.input-box input:focus {
  border: 2px solid #0880ae;
  padding: 0 0px 0px 15px;
}
.input-box .details {
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