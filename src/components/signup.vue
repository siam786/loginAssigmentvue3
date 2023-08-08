<template>
  <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <img
        class="mx-auto h-10 w-auto"
        src="https://vogal-demo.myshopify.com/cdn/shop/files/logo-dark_80x@2x.png?v=1673416733"
        alt="Seven Rings"
      />
      <h2
        class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900"
      >
        Register in to your account
      </h2>
    </div>
    <!-- login form start -->
    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <form
        @submit.prevent="signupHandler"
        class="space-y-6 p-6 border border-black h-full w-full bg-red-200 rounded-md bg-clip-padding backdrop-filter backdrop-blur-sm bg-opacity-0 border border-gray-100"
        action=""
      >
        <div>
          <label
            for="email"
            class="block text-md font-medium leading-6 text-white"
            >Email address</label
          >
          <div class="mt-2">
            <input
              v-model="form.email"
              placeholder="jhon@doe.com"
              id="email"
              name="email"
              type="email"
              autocomplete="email"
              required
              class="block w-full rounded-md border-0 p-2 text-black shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
            <span
              class="error text-xs italic text-red-600"
              :class="formError.email ? '' : 'hidden'"
              >* Required</span
            >
          </div>
        </div>

        <div>
          <div class="flex items-center justify-between">
            <label
              for="password"
              class="block text-md font-medium leading-6 text-white"
              >Password</label
            >
          </div>
          <div class="mt-2">
            <input
              v-model="form.password"
              id="password"
              placeholder="*********"
              name="password"
              type="password"
              autocomplete="current-password"
              required
              class="block w-full rounded-md border-0 p-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
            <span
              class="error text-xs italic text-red-600"
              :class="formError.password ? '' : 'hidden'"
              >* Required</span
            >
          </div>
        </div>

        <div>
          <div class="flex items-center justify-between">
            <label
              for="confirm_password"
              class="block text-md font-medium leading-6 text-white"
              >Confirm Password</label
            >
          </div>
          <div class="mt-2">
            <input
              v-model="form.confirm_password"
              id="confirm_password"
              placeholder="*********"
              name="password"
              type="password"
              autocomplete="current-password"
              required
              class="block w-full rounded-md border-0 p-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
            <span
              class="error text-xs italic text-red-600"
              :class="formError.confirm_password ? '' : 'hidden'"
              >* Does not match</span
            >
          </div>
        </div>

        <div>
          <button
            type="submit"
            class="flex w-full justify-center rounded-md bg-red-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-red-800 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
            :disabled="btnDisabled"
          >
            Register
          </button>
         
        </div>
      </form>

      <p
        class="mt-10 text-center text-lg text-black-500 text-red-500 bg-slate-500 h-full w-full bg-green-200 rounded-md bg-clip-padding backdrop-filter backdrop-blur-sm bg-opacity-0 border border-gray-100"
      >
        Account Create?
        <a
          @click.prevent="$emit('funcChange')"
          href="#"
          class="font-semibold leading-6 text-red-600 hover:text-white"
          >Login here</a
        >
      </p>
    </div>
    <!-- login form end -->
  </div>
</template>

<script setup>
import { reactive,ref } from "vue";
const emit = defineEmits(["funcSignup", "funcChange"]);
const form = reactive({
  email: "",
  password: "",
  confirm_password: "",
});
const formError = reactive({
  email: false,
  password: false,
  confirm_password: false,
});
const loading = ref(false);
const btnDisabled = ref(false);
const loginOK = ref(false);
const signupHandler = () => {
  console.log(form);

  if (form.email == "") {
    formError.email = true;
  } else {
    formError.email = false;
  }
  if (form.password == "") {
    formError.password = true;
  } else {
    formError.password = false;
  }
  if (form.password != form.confirm_password) {
    formError.confirm_password = true;
  } else {
    formError.confirm_password = false;
  }

  if (formError.email || formError.password || formError.confirm_password)
    return;

  loading.value = true;
  btnDisabled.value = true;
  // simulate api execution delay
  setTimeout(() => {
    loading.value = false;
    loginOK.value = true;
    setTimeout(() => {
      loginOK.value = false;
      emit("funcSignup", form);
    }, 500);
  }, 1000);
};
</script>

<style></style>
