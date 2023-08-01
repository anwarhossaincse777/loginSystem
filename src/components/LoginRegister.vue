<script setup>
import {reactive, ref} from "vue";


const person = reactive(
    {
      Username: {value: '', type: 'text', placeholder: 'User Name'},
      password: {value: '', type: 'password', placeholder: 'password'},
    }
)

const newPerson = reactive(
    {
      confirmPassword: ''
    }
)

const confirmPass = ref(false);
const rButton=ref(true);
const largeScreen=ref(true);
const styleImage=ref('w-1/2')


function login() {

  if (person.Username.value && person.password.value === newPerson.confirmPassword) {

    alert("Successfully logged In")
    largeScreen.value=false;
    styleImage.value='w-full';

  } else {

    alert("Password not match")
  }

}


function register() {
  if (newPerson.confirmPassword.length === 0) {
    confirmPass.value = !confirmPass.value;
  } else {
    if (person.password.value === newPerson.confirmPassword) {

      alert("Registration Successfully Completed")
      confirmPass.value = false;
      rButton.value = false;
    } else {
      alert("Password not match")
    }
  }
}


</script>


<template>
  <section class="flex h-screen w-full">
    <div :class="styleImage"
         style="background-image: url(https://images.unsplash.com/photo-1690555575753-7aa27df96b52?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=774&q=80); background-repeat: no-repeat; background-size: cover;">
      <h1 class="mb-5 text-2xl mt-10 ml-10 text-white">Kosmos!</h1>
    </div>
    <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200" v-show="largeScreen">
      <h2 class="mb-5 text-xl">Login or register</h2>
      <h2 class="mb-5 text-xl">{{ person }}</h2>
      <h2 class="mb-5 text-xl">{{ newPerson }}</h2>
      <div class="w-full max-w-xs">
        <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
          <div class="mb-4" v-for="(value,key,index) in person" :key="key">
            <label class="block text-gray-700 text-sm font-bold mb-2">
              {{ key }}
            </label>
            <input :type="person[key].type" v-model="person[key].value"
                   class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                   :placeholder="person[key].placeholder">
          </div>

          <div v-show="confirmPass" class="mb-4">
            <label class="block text-gray-700 text-sm font-bold mb-2">
              Confirm Password
            </label>
            <input v-model="newPerson.confirmPassword" type="password"
                   class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                   placeholder="Confirm password">
          </div>

          <div class="flex items-center justify-between">
            <button @click.prevent="login()"
                    class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                    type="button">
              Sign In
            </button>

            <button v-show="rButton" @click.prevent="register()"
                    class="inline-block align-baseline font-bold text-sm text-orange-600 hover:text-orange-800">
              Or Register
            </button>

          </div>
        </form>
        <p class="text-center text-gray-500 text-xs">
          &copy;2020 Acme Corp. All rights reserved.
        </p>
      </div>
    </div>
  </section>
</template>


<style scoped>

</style>