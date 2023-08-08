<script setup>
import { ref, reactive } from "vue";
const isRegister = ref(false);
const isAuth = ref(false);
const isRejectToLogin = ref(false);
const register = reactive({
  username: "",
  password: "",
  confirmPassword: "",
  errorMsgUsername: "",
  errorMsgPass: "",
  meessage: "",
});

// const auth = {
//   username: "abcd",
//   password: 123,
// };

function isRegistration() {
  if (
    "" !== register.username &&
    "" !== register.password &&
    "" !== register.confirmPassword
  ) {
    if (register.password == register.confirmPassword) {
      localStorage.setItem("authInfo", JSON.stringify(register));
      register.meessage = "Thank you for registering";
      isAuth.value = true;
      isRegister.value = false;
    }
  }
  if (isRegister.value) {
    validation();
  }

  isRegister.value = true;
}

function validation() {
  register.errorMsgUsername = register.username
    ? ""
    : "Username filed is required!";

  register.errorMsgPass = register.password
    ? ""
    : "Password filed is required!";

  if (isRegister.value) {
    register.errorMsgConfirm = "Password doesn't mach!";
  }
}

function isLogin() {
  validation();
  let auth = JSON.parse(localStorage.getItem("authInfo"));
  isRegister.value = false;
  if ("" !== register.username && "" !== register.password) {
    if (
      register.username === auth?.username &&
      register.password === auth?.password
    ) {
      register.meessage = "You have successfully login.";
      isAuth.value = true;
      isRegister.value = false;
    }
    isRejectToLogin.value = true;
  }
}

function logout() {
  isAuth.value = false;
  isRegister.value = false;

  register.username = "";
  register.password = "";
  register.confirmPassword = "";
  register.errorMsgUsername = "";
  register.errorMsgPass = "";
  register.meessage = "";
  isRejectToLogin.value = false;
}
</script>

<template>
  <section class="flex h-screen w-full">
    <div
      class="w-1/2"
      style="
        background-image: url(https://images.unsplash.com/photo-1690555575753-7aa27df96b52?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80);
        background-repeat: no-repeat;
        background-size: cover;
      "
    >
      <h1 class="mb-5 text-2xl mt-10 ml-10 text-white">Kosmos!</h1>
    </div>
    <div
      class="w-1/2 flex flex-col justify-center items-center bg-gray-200"
      v-show="!isAuth"
    >
      <p>{{ register }}</p>

      <h2 class="mb-5 text-xl">Login or register</h2>
      <div class="w-full max-w-xs">
        <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
          <!-- Alert message -->
          <div
            v-show="isRejectToLogin"
            class="px-5 py-2 mb-4 bg-red-100 border border-red-200 rounded-lg"
          >
            ❗ Please provide valid credentials or
            <span
              @click.prevent="isRegistration()"
              class="font-bold text-green-600 cursor-pointer"
              >Register</span
            >
          </div>
          <div class="mb-4">
            <label
              class="block text-gray-700 text-sm font-bold mb-2"
              for="username"
            >
              Username
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="username"
              type="text"
              placeholder="Username"
              v-model="register.username"
            />
            <p class="text-red-500" v-show="register.errorMsgUsername">
              {{ register.errorMsgUsername }}
            </p>
          </div>
          <div class="mb-6">
            <label
              class="block text-gray-700 text-sm font-bold mb-2"
              for="password"
            >
              Password
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
              id="password"
              type="password"
              placeholder="******************"
              v-model="register.password"
            />
            <p class="text-red-500" v-show="register.errorMsgPass">
              {{ register.errorMsgPass }}
            </p>
          </div>
          <div class="mb-6" v-show="isRegister">
            <label
              class="block text-gray-700 text-sm font-bold mb-2"
              for="confirm_password"
            >
              Confirm Password
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
              id="confirm_password"
              type="confirm_password"
              placeholder="******************"
              v-model="register.confirmPassword"
            />
            <p class="text-red-500" v-show="register.errorMsgConfirm">
              {{ register.errorMsgConfirm }}
            </p>
          </div>
          <div class="flex items-center justify-between">
            <button
              class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              type="button"
              @click="isLogin()"
            >
              Sign In
            </button>
            <a
              class="inline-block align-baseline font-bold text-sm text-orange-600 hover:text-orange-800"
              href="#"
              @click="isRegistration()"
            >
              Or Register
            </a>
          </div>
        </form>
        <p class="text-center text-gray-500 text-xs">
          &copy;2020 Acme Corp. All rights reserved.
        </p>
      </div>
    </div>
    <div
      class="w-1/2 flex flex-col justify-center items-center bg-gray-200"
      v-show="isAuth"
    >
      <h2 class="mb-5 text-xl text-green-500">{{ register.meessage }}</h2>
      <p>Username: {{ register.username }}</p>
      <p>Password: {{ register.password }}</p>
      <button
        class="mt-5 mb-5 cursor-pointer bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        @click="logout()"
      >
        Logout
      </button>
      <div class="w-full max-w-xs">
        <p class="text-center text-gray-500 text-xs">
          &copy;2020 Acme Corp. All rights reserved.
        </p>
      </div>
    </div>
  </section>
</template>
<style scoped></style>
