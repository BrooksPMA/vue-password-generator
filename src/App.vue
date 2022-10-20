<template>
  <div class="flex items-center justify-center h-screen font-sans font-medium">
    <div
      class="p-4 w-full max-w-sm bg-white rounded-lg border border-gray-200 shadow-2xl sm:p-6 md:p-8 dark:bg-gray-800 dark:border-gray-700"
    >
      <h5 class="sm:text-3xl font-medium text-gray-900 dark:text-white">
        Password Generator
      </h5>
      <div class="sm:mt-8 relative w-full">
        <input
          placeholder="CLICK GENERATE"
          type="text"
          v-model="passwordInput"
          v-on:focus="$event.target.select()"
          ref="myinput"
          readonly
          class="bg-gray-200 border-none border-gray-300 rounded text-gray-900 text-sm block w-full p-2 sm:p-5 dark:bg-gray-600 dark:border-none dark:placeholder-gray-400 placeholder:text-center dark:text-white dark:focus:outline-none"
        />
        <button
          @click="copy"
          class="absolute top-0 right-0 p-2 sm:p-5 text-sm rounded text-gray-600 hover:text-gray-700 dark:text-gray-400 dark:hover:text-gray-500"
        >
          <svg
            class="w-auto h-5"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M8 16H6a2 2 0 01-2-2V6a2 2 0 012-2h8a2 2 0 012 2v2m-6 12h8a2 2 0 002-2v-8a2 2 0 00-2-2h-8a2 2 0 00-2 2v8a2 2 0 002 2z"
            ></path>
          </svg>
          <span class="sr-only">Copy</span>
        </button>
      </div>
      <div class="mt-4">
        <h1 class="flex pl-2 text-xs text-gray-400 dark:text-gray-500">
          LENGTH:
          <p class="pl-1 text-gray-700 dark:text-white">
            {{ passwordLength }}
          </p>
        </h1>
        <div
          class="flex items-center bg-gray-200 border-none border-gray-300 rounded text-gray-900 text-sm w-full p-2 sm:p-3 dark:bg-gray-600 dark:border-none dark:placeholder-gray-400 placeholder:text-center dark:text-white dark:focus:outline-none"
        >
          <p class="pr-3">4</p>
          <input
            class="w-full h-1 bg-gray-300 rounded-lg appearance-none cursor-pointer dark:bg-gray-700"
            type="range"
            min="4"
            max="16"
            step="1"
            v-model="passwordLength"
          />
          <p class="pl-3">16</p>
        </div>
      </div>
      <div class="mt-4">
        <h1 class="flex pl-2 text-xs text-gray-400 dark:text-gray-500">
          SETTINGS
        </h1>
        <div
          class="flex items-center mb-2 bg-gray-200 border-none border-gray-300 rounded text-gray-900 text-sm w-full p-2 sm:p-3 dark:bg-gray-600 dark:border-none dark:placeholder-gray-400 placeholder:text-center dark:text-white dark:focus:outline-none"
          @click="includeLowercase = !includeLowercase"
        >
          <input
            type="checkbox"
            class="w-4 h-4 text-blue-900 bg-gray-100 rounded border-gray-300 focus:ring-blue-800 dark:focus:ring-blue-900 dark:ring-offset-gray-800 dark:bg-gray-700 dark:border-gray-600"
            v-model="includeLowercase"
          />
          <label
            for="checkbox"
            class="ml-2 text-lg font-normal text-gray-900 dark:text-gray-400"
            >Include Lowercase</label
          >
        </div>
        <div
          class="flex items-center mb-2 bg-gray-200 border-none border-gray-300 rounded text-gray-900 text-sm w-full p-2 sm:p-3 dark:bg-gray-600 dark:border-none dark:placeholder-gray-400 placeholder:text-center dark:text-white dark:focus:outline-none"
          @click="includeUppercase = !includeUppercase"
        >
          <input
            type="checkbox"
            class="w-4 h-4 text-blue-900 bg-gray-100 rounded border-gray-300 focus:ring-blue-800 dark:focus:ring-blue-900 dark:ring-offset-gray-800 dark:bg-gray-700 dark:border-gray-600"
            v-model="includeUppercase"
          />
          <label
            for="checkbox"
            class="ml-2 text-lg font-normal text-gray-900 dark:text-gray-400"
            >Include Uppercase</label
          >
        </div>
        <div
          class="flex items-center mb-2 bg-gray-200 border-none border-gray-300 rounded text-gray-900 text-sm w-full p-2 sm:p-3 dark:bg-gray-600 dark:border-none dark:placeholder-gray-400 placeholder:text-center dark:text-white dark:focus:outline-none"
          @click="includeNumbers = !includeNumbers"
        >
          <input
            type="checkbox"
            class="w-4 h-4 text-blue-900 bg-gray-100 rounded border-gray-300 focus:ring-blue-800 dark:focus:ring-blue-900 dark:ring-offset-gray-800 dark:bg-gray-700 dark:border-gray-600"
            v-model="includeNumbers"
          />
          <label
            for="checkbox"
            class="ml-2 text-lg font-normal text-gray-900 dark:text-gray-400"
            >Include Numbers</label
          >
        </div>
        <div
          class="flex items-center mb-2 bg-gray-200 border-none border-gray-300 rounded text-gray-900 text-sm w-full p-2 sm:p-3 dark:bg-gray-600 dark:border-none dark:placeholder-gray-400 placeholder:text-center dark:text-white dark:focus:outline-none"
          @click="includeSymbols = !includeSymbols"
        >
          <input
            type="checkbox"
            class="w-4 h-4 text-blue-900 bg-gray-100 rounded border-gray-300 focus:ring-blue-800 dark:focus:ring-blue-900 dark:ring-offset-gray-800 dark:bg-gray-700 dark:border-gray-600"
            v-model="includeSymbols"
          />
          <label
            for="checkbox"
            class="ml-2 text-lg font-normal text-gray-900 dark:text-gray-400"
            >Include Symbols</label
          >
        </div>
      </div>
      <button
        @click="generatePassword"
        type="button"
        class="text-white bg-gradient-to-br from-purple-300 to-blue-400 dark:from-purple-600 dark:to-blue-500 hover:bg-gradient-to-bl font-medium rounded-lg text-sm px-2 py-5 mt-2 sm:px-5 sm:py-5 sm:mt-5 text-center w-full disabled:cursor-not-allowed disabled:opacity-25 disabled:hover:bg-gradient-to-br"
        :disabled="disabledButton"
      >
        GENERATE PASSWORD
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      passwordInput: '',
      passwordLength: 8,
      includeLowercase: true,
      includeUppercase: false,
      includeNumbers: false,
      includeSymbols: false,
      chars: '',
      lowerChars: 'abcdefghijklmnopqrstuvwxyz',
      upperChars: 'ABCDEFGHIJKLMNOPQRSTUVWXYZ',
      numbers: '0123456789',
      symbols: '~`!@#$%^&*()_-+={[}]|:;"<,>.?/',
    };
  },
  methods: {
    generatePassword() {
      this.passwordInput = '';
      this.chars = '';

      this.checkboxToggled(this.includeLowercase, this.lowerChars);
      this.checkboxToggled(this.includeUppercase, this.upperChars);
      this.checkboxToggled(this.includeNumbers, this.numbers);
      this.checkboxToggled(this.includeSymbols, this.symbols);

      for (let i = 0; i < this.passwordLength; i++) {
        let randomChar = Math.floor(Math.random() * this.chars.length);
        this.passwordInput += this.chars[randomChar];
      }
    },
    checkboxToggled(checkboxName, typeName) {
      if (checkboxName) {
        this.chars = this.chars.concat(typeName);
      }
    },
    copy() {
      this.$refs.myinput.focus();
      document.execCommand('copy');
    },
  },
  computed: {
    disabledButton() {
      if (
        !this.includeLowercase &&
        !this.includeUppercase &&
        !this.includeNumbers &&
        !this.includeSymbols
      ) {
        return true;
      }
      return false;
    },
  },
};
</script>

<style></style>
