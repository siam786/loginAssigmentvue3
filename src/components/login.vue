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
        Login in to your account
      </h2>
    </div>
    <!-- login form start -->
    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <form
        @submit.prevent="loginHandler"
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
              id="email"
              name="email"
              type="email"
              placeholder="jhon@doe.com"
              autocomplete="email"
              required
              class="block w-full rounded-md border-0 p-2 text-black shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
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
              name="password"
              type="password"
              placeholder="********"
              autocomplete="current-password"
              required
              class="block w-full rounded-md border-0 p-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
            />
          </div>
        </div>

        <div>
          <button
            type="submit"
            class="flex w-full justify-center rounded-md bg-red-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-red-800 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          >
            Sign in
          </button>
        </div>
      </form>

      <p
        class="mt-10 text-center text-lg text-black-500 text-red-500 bg-slate-500 h-full w-full bg-green-200 rounded-md bg-clip-padding backdrop-filter backdrop-blur-sm bg-opacity-0 border border-gray-100"
      >
        Not a member?
        <a @click.prevent="$emit('funcChange')"
          href="#"
          class="font-semibold leading-6 text-red-600 hover:text-white"
          >Register Here</a
        >
      </p>
    </div>
    <!-- login form end -->
  </div>
</template>

<script setup>
import { reactive, ref } from "vue";

const props = defineProps({
  logindata: {
    type: Object,
  },
});

const emit = defineEmits(["funcLogin", "funcChange"]);

const loading = ref(false);
const btnDisabled = ref(false);
const loginFailed = ref(false);
const loginOK = ref(false);

const form = reactive({
  email: "",
  password: "",
});

const formError = reactive({
  email: false,
  password: false,
});

//function - validate required, check login data
const loginHandler = () => {
  loginFailed.value = false;
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
  if (formError.email || formError.password) return;

  if (
    form.email != props.logindata.email ||
    form.password != props.logindata.password
  ) {
    loginFailed.value = true;
    loginOK.value = false;
    return;
  }

  btnDisabled.value = true;
  loading.value = true;
  loginFailed.value = false;

  // simulate api execution delay
  setTimeout(() => {
    loading.value = false;
    loginOK.value = true;
    setTimeout(() => {
      loginFailed.value = false;
      emit("funcLogin", form);
    }, 500);
  }, 1000);
};
</script>

<style></style>
