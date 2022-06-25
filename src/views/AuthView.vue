<template>
  <div class="home">
    <h1>LeadHit</h1>
    <form class="id-form">
      <MDBInput @input="inputHandler" class="mb-3" color="danger" counter :maxlength="24" label="ID сайта" v-model="userInput" />
      <span ref="errorRef" class="form-text"> id сайта должен содержать 24 символа </span>
      <MDBBtn @click.prevent="submitHandler" type="submit" color="primary" rounded>Войти</MDBBtn>
    </form>
  </div>
</template>

<script>
import { MDBInput, MDBBtn } from "mdb-vue-ui-kit";
import { ref } from "vue";
import { useRouter } from "vue-router";
export default {
  name: "AuthView",
  components: {
    MDBInput,
    MDBBtn,
  },
  setup() {
    const userInput = ref("");
    const errorRef = ref(null);
    const router = useRouter();

    const showErrorMessage = () => {
      errorRef.value.classList.add("form-text--active");
    };

    const hideErrorMessage = () => {
      errorRef.value.classList.remove("form-text--active");
    };

    const sendRequestToServer = async () => {
      const response = await fetch("https://track-api.leadhit.io/client/test_auth", {
        method: "GET",
        headers: {
          "Api-Key": "5f8475902b0be670555f1bb3:eEZn8u05G3bzRpdL7RiHCvrYAYo",
          "Leadhit-Site-Id": userInput.value,
        },
      });
      const reply = await response.json();
      const { message } = reply;
      if (message === "ok") {
        console.log("success");
        localStorage.setItem("leadhit-site-id", "5f8475902b0be670555f1bb3");
        router.push("/analytics");
      } else {
        console.log("something went wrong");
      }
    };

    const submitHandler = () => {
      if (userInput.value.length !== 24) {
        showErrorMessage();
      } else if (userInput.value.length === 24) {
        sendRequestToServer();
      }
    };

    const inputHandler = () => {
      if (errorRef.value.classList.contains("form-text--active")) {
        hideErrorMessage();
      }
    };

    return { userInput, submitHandler, errorRef, inputHandler };
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
