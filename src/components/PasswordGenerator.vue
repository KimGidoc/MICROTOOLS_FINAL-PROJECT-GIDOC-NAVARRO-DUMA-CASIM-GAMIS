
<template>
    <div class="col-md-9 p-5" v-if="showPasswordGeneratorComponent">
        <div class="text-center mb-5">
            <h1>Random Password Generator</h1>
        </div>
        <div class="form-group">
            <label style="font-weight: bold;">Input password length:</label>
            <input type="number" id="length" min="6" max="30" v-model="passwordLength" class="form-control mt-2 w-50" placeholder="Minimum of 6 characters" >
        </div>
        <div class="container">
            <div class="row mt-3">
                <div class="col-md-6">
                    <div class="form-check">
                        <input class="form-check-input" type="checkbox" value="" id="includeUppercase" v-model="includeUppercase">
                        <label class="form-check-label" for="flexCheckDefault">
                            Include Uppercase Letters
                        </label>
                    </div>
                    <div class="form-check">
                        <input class="form-check-input" type="checkbox" value="" id="includeNumbers" v-model="includeNumbers">
                        <label class="form-check-label" for="flexCheckDefault">
                            Include numbers
                        </label>
                    </div>
                    <div class="form-check">
                        <input class="form-check-input" type="checkbox" value="" id="includeSymbols" v-model="includeSymbols">
                        <label class="form-check-label" for="flexCheckDefault">
                            Include Symbols
                        </label>
                    </div>
                </div>
                <div class="col-md-6">
                    <div class="mt-3 d-flex justify-content-center">
                        <button class="btn btn-primary" @click="generatePassword">Generate Password</button>
                    </div>
                </div>
            </div>
        </div>

        

        <div v-if="generatedPassword" class="mt-3">
            <h5>Generated Password:</h5>
            <textarea style="font-weight: bold; font-size: 30px" class="form-control text-center p-5" rows="1" :value="generatedPassword" readonly></textarea>
            <div class="d-flex justify-content-end mt-2">
                <button @click="copyToClipboard" class="btn btn-success">Copy</button>
            </div>
        </div>
             
    </div>
</template>

<script>
export default {
    props: ['showPasswordGeneratorComponent'],
  data() {
    return {
      passwordLength: '6',
      includeUppercase: true,
      includeNumbers: true,
      includeSymbols: true,
      generatedPassword: '',
    };
  },
  methods: {
    generatePassword() {
      const lowercaseLetters = 'abcdefghijklmnopqrstuvwxyz';
      const uppercaseLetters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
      const numbers = '0123456789';
      const symbols = '!@#$%^&*()-=_+[]{}|;:,.<>?/';

      let characters = lowercaseLetters;
      if (this.includeUppercase) characters += uppercaseLetters;
      if (this.includeNumbers) characters += numbers;
      if (this.includeSymbols) characters += symbols;

      let password = '';
      for (let i = 0; i < this.passwordLength; i++) {
        const randomIndex = Math.floor(Math.random() * characters.length);
        password += characters.charAt(randomIndex);
      }

      this.generatedPassword = password;
    },
    copyToClipboard() {
      const textarea = document.createElement('textarea');
      textarea.value = this.generatedPassword;
      document.body.appendChild(textarea);
      textarea.select();
      document.execCommand('copy');
      document.body.removeChild(textarea);
      alert('Password copied to clipboard.');
    },
  },
};
</script>