<script setup>
import { ref, reactive } from "vue";

const hidden = ref("hidden");
const block = ref("block");
const message = ref("hidden");
const loginmessage = ref("hidden");
const signup = reactive({
  username: "",
  password: "",
  confirm_password: "",
  errorUser: "",
  errorPassword: "",
  errorConfirmPassword: "",
});

const myData = {
  username: "abc",
  password: "123",
  confirm_password: "123",
};

function registeration() {
  if (
    "" !== signup.username &&
    "" !== signup.password &&
    "" !== signup.confirm_password
  ) {
    alert("ABC");
  }

  if ("" === signup.username) {
    hidden.value = "block";
    signup.errorUser = "Please Enter User Name";
  }

  if ("" === signup.password) {
    hidden.value = "block";
    signup.errorPassword = "Please Enter Password";
  }

  if ("" === signup.confirm_password) {
    hidden.value = "block";
    signup.errorConfirmPassword = "Please Retype Password";
  }
  if (
    signup.password === myData.password &&
    signup.confirm_password === myData.confirm_password
  ) {
    block.value = "hidden";
    message.value = "block";
  } else {
    hidden.value = "block";
    signup.errorConfirmPassword = "Password or Confirm password doesnot match.";
  }
}

function back() {
  block.value = "block";
  message.value = "hidden";
  hidden.value = "hidden";
}

function signIn() {
  if (
    signup.password === myData.password &&
    signup.username === myData.username
  ) {
    block.value = "hidden";
    loginmessage.value = "block";
  } else {
    alert("Error");
  }
}

function logout() {
  block.value = "block";
  loginmessage.value = "hidden";
  hidden.value = "hidden";
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
      :class="block"
    >
      <p>{{ signup }}</p>
      <h2 class="mb-5 text-xl">Login or register</h2>
      <div class="w-full max-w-xs">
        <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
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
              v-model="signup.username"
            />
            <p class="text-red-500" :class="hidden">{{ signup.errorUser }}</p>
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
              v-model="signup.password"
            />
            <p class="text-red-500" :class="hidden">
              {{ signup.errorPassword }}
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
              v-model="signup.confirm_password"
              :class="hidden"
            />
            <p class="text-red-500" :class="hidden">
              {{ signup.errorConfirmPassword }}
            </p>
          </div>

          <div class="flex items-center justify-between">
            <button
              class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              type="button"
              @click="signIn()"
            >
              Sign In
            </button>
            <a
              class="inline-block align-baseline font-bold text-sm text-orange-600 hover:text-orange-800"
              href="#"
              @click="registeration()"
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
      :class="message"
    >
      <h2 class="mb-5 text-xl text-green-500">Thank you for registering</h2>
      <p>Username: {{ signup.username }}</p>
      <p>Password: {{ signup.password }}</p>
      <button
        class="mt-5 mb-5 cursor-pointer bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        @click="back()"
      >
        Back
      </button>
      <div class="w-full max-w-xs">
        <p class="text-center text-gray-500 text-xs">
          &copy;2020 Acme Corp. All rights reserved.
        </p>
      </div>
    </div>

    <div
      class="w-1/2 flex flex-col justify-center items-center bg-gray-200"
      :class="loginmessage"
    >
      <h2 class="mb-5 text-xl text-green-500">Thank you for login</h2>
      <p>Username: {{ signup.username }}</p>
      <p>Password: {{ signup.password }}</p>
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
