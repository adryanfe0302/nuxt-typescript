<template>
     <div class="min-h-screen flex items-center justify-center bg-gray-50 py-12 px-4 sm:px-6 lg:px-8">
        <div class="max-w-md w-full">
            <div>
            <img class="mx-auto h-12 w-auto" src="https://tailwindui.com/img/logos/v1/workflow-mark-on-white.svg" alt="Workflow">
            <h2 class="mt-6 text-center text-3xl leading-9 font-extrabold text-gray-900">
                Sign in to your account
            </h2>
            <p class="mt-2 text-center text-sm leading-5 text-gray-600">
                
            </p>
            </div>
            <form class="mt-8" action="#" method="POST">
            <input type="hidden" name="remember" value="true">
            <div class="rounded-md shadow-sm">
                <div>
                <input v-model="formUsername" aria-label="User Name" name="text" type="text" required class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:shadow-outline-blue focus:border-blue-300 focus:z-10 sm:text-sm sm:leading-5" placeholder="User Name">
                </div>
                <div class="-mt-px">
                <input v-model="formPassword" aria-label="Password" name="password" type="password" required class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-b-md focus:outline-none focus:shadow-outline-blue focus:border-blue-300 focus:z-10 sm:text-sm sm:leading-5" placeholder="Password">
                </div>
            </div>

            <div class="mt-6 flex items-center justify-between">
                <div class="flex items-center text-sm err-msg">
                
                </div>

                <div class="text-sm leading-12">
                <div class="flex items-center text-sm err-msg">
                    {{this.formError}}
                </div>
                </div>
            </div>

            <div class="mt-6">
                <button type="submit" class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm leading-5 font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-500 focus:outline-none focus:border-indigo-700 focus:shadow-outline-indigo active:bg-indigo-700 transition duration-150 ease-in-out" v-on:click="clickLogin">
                <span class="absolute left-0 inset-y-0 flex items-center pl-3">
                    <svg class="h-5 w-5 text-indigo-500 group-hover:text-indigo-400 transition ease-in-out duration-150" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd" d="M5 9V7a5 5 0 0110 0v2a2 2 0 012 2v5a2 2 0 01-2 2H5a2 2 0 01-2-2v-5a2 2 0 012-2zm8-2v2H7V7a3 3 0 016 0z" clip-rule="evenodd" />
                    </svg>
                </span>
                Sign in
                </button>
                </div>
            </form>
        </div>
       
        </div>
</template>

<script lang='ts'>
export default {
    head: {
        title: 'Login Page'
    },
    data() {
      return {
        formError: null,
        formUsername: '',
        formPassword: ''
      }
    },
    methods: {
        clickLogin (e) {
          e.preventDefault();
            try {
                if (this.formUsername === '' && this.formPassword === '') {
                   this.formError = 'Masukkan password & email anda'

                } else if (this.formUsername === '' && this.formPassword !== '') {
                   this.formError = 'Masukkan email anda'
                } else if (this.formUsername !== '' && this.formPassword === '') {
                   this.formError = 'Masukkan password anda'
                } else {
                   window.sessionStorage.setItem('statusLogin', 'true')
                   window.sessionStorage.setItem('email', this.formUsername)
                   this.formError = ''
                   this.$router.push('/dashboard')
                }                
            } catch (e) {
                this.formError = e.message
            }
        }
    },
    mounted() {
        if (window.sessionStorage.getItem('statusLogin') === 'true') {
            this.$router.push('/dashboard')
        }
    },
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.err-msg {
  font-size: 12px;
  color: red;
}

</style>