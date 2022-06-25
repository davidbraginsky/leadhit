<template>
  <div class="home">
    <h1>LeadHit</h1>
    <form class="id-form">
      <MDBInput class="mb-3" color="danger" counter :maxlength="24" label="ID сайта" v-model="userInput" />
      <span ref="errorRef" class="form-text"> Site ID must be 24 characters </span>
      <MDBBtn @click.prevent="submitHandler" type="submit" color="primary" rounded>Войти</MDBBtn>
    </form>
  </div>
</template>

<script>
import { MDBInput, MDBBtn } from "mdb-vue-ui-kit";
import { ref } from "vue";
export default {
  name: "AuthView",
  components: {
    MDBInput,
    MDBBtn,
  },
  setup() {
    const userInput = ref("");
    const errorRef = ref(null);

    const submitHandler = () => {
      if (userInput.value.length !== 24) {
        console.dir(errorRef.value.classList.add("form-text--active"));
      } else if (userInput.value.length === 24) {
        console.log("user input is correct length");
      }
    };

    return { userInput, submitHandler, errorRef };
  },
};
</script>

<style scoped>
.id-form {
  max-width: 500px;
  margin: 0 auto;
}

.form-text {
  color: red;
  display: none;
}

.form-text--active {
  display: block;
}

.id-input {
  margin-bottom: 16px;
}
</style>
