<template>
  <div>
    <Form />
  </div>
</template>

<script>
import Form from "./components/RegistrationForm.vue";
export default {
  name: "App",
  components: {
    Form,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=IBM+Plex+Sans");
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  height: 100vh;
  background-color: #0093e9;
  background-image: linear-gradient(160deg, #0093e9 0%, #80d0c7 100%);
}
* {
  font-family: "IBM Plex Sans" !important;
}
</style>
