<script setup>
import { reactive } from 'vue';

const form = reactive({
    email: '',
    password: '',
    confirm_password: ''
})

const emit = defineEmits(['funcLogout'])

const logoutHandler = ()=>{
    emit('funcLogout')
}

</script>


<template>

    <div class="">
        <div class="w-full flex flex-col bg-blue-100 h-screen  justify-center items-center">
            <div class="h-1/2 flex justify-center items-end">
                <img
        class="mx-auto h-10 w-auto mb-5"
        src="https://vogal-demo.myshopify.com/cdn/shop/files/logo-dark_80x@2x.png?v=1673416733"
        alt="Seven Rings"
      />
            </div>
            <div class="h-1/2 w-1/4 max-w-lg flex flex-col justify-start items-center">
                <div class="flex justify-center items-center bg-white w-full p-5">
                    <h1 class="text-lg">Welcome</h1>
                </div>
                <button type="submit" class="flex w-full justify-center rounded-md bg-red-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-red-800 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 mt-5">
                    <a @click.prevent="logoutHandler()" href="" class="p-1 text-2xl text-white hover:text-white" >Logout</a>
                </button>

            </div>
        </div>
    </div>



</template>

<style scoped></style>
