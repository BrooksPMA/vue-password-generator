<template>
  <div>
    <h2>Your password is:</h2>
    <input
      placeholder="Your password will be here"
      type="text"
      v-model="passwordInput"
    />
    <div style="display: block">
      <input type="checkbox" v-model="checkedSymbols" />
      <label for="checkbox">Use symbols</label>
    </div>
    <button @click="generatePassword">Generate password</button>
  </div>
</template>

<script>
import { chars, symbols } from './api/characters';

export default {
  name: 'App',
  data() {
    return {
      passwordInput: '',
      passwordLength: 8,
      checkedSymbols: false,
      generatedPassword: '',
      setChars: chars,
    };
  },
  methods: {
    generatePassword() {
      this.passwordInput = '';
      this.generatedPassword = '';

      if (this.checkedSymbols) {
        this.setChars = chars.concat(symbols);
      } else {
        this.setChars = chars;
      }

      for (let i = 0; i < this.passwordLength; i++) {
        let randomChar = Math.floor(Math.random() * this.setChars.length);
        this.generatedPassword += this.setChars[randomChar];
      }
      this.passwordInput = this.generatedPassword;
    },
  },
};
</script>

<style></style>
