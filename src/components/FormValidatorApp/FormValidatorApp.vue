<template>
  <div class="form-validator-body">
    <div class="container">
      <form class="form" v-on:submit.prevent="handleSubmit">
        <h2>Register with us</h2>
        <div class="form-control" v-bind:class="usernameErrClass">
          <label for="username">Username</label>
          <input type="text" v-model="username" placeholder="Enter username" />
          <small>{{ usernameErrMsg }}</small>
        </div>
        <div class="form-control" v-bind:class="emailErrClass">
          <label for="email">Email</label>
          <input type="text" v-model="email" placeholder="Enter email" />
          <small>{{ emailErrMsg }}</small>
        </div>
        <div class="form-control" v-bind:class="passwordErrClass">
          <label for="password">Password</label>
          <input type="password" v-model="password" placeholder="Enter password" />
          <small>{{ passwordErrMsg }}</small>
        </div>
        <div class="form-control" v-bind:class="password2ErrClass">
          <label for="password2">Confirm password</label>
          <input type="password" v-model="password2" placeholder="Enter password again" />
          <small>{{ password2ErrMsg }}</small>
        </div>
        <button>Submit</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FormValidatorApp',
  data() {
    return {
      username: '',
      usernameErrMsg: '',
      usernameErrClass: '',
      email: '',
      emailErrMsg: '',
      emailErrClass: '',
      password: '',
      passwordErrMsg: '',
      passwordErrClass: '',
      password2: '',
      password2ErrMsg: '',
      password2ErrClass: '',
    }
  },
  methods: {
    handleSubmit(event) {
      if (!this.checkRequired(['username', 'email', 'password', 'password2'])) {
        this.checkLength('username', 3, 15)
        this.checkLength('password', 6, 25)
        this.checkEmail(this.email)
        this.checkPasswordMatch(this.password, this.password2)
      }
    },
    checkRequired(formFieldNames) {
      let isRequired = false
      formFieldNames.forEach((fieldName) => {
        if (this[fieldName].trim() === '') {
          this.showError(
            fieldName,
            `${this.capitalizeFirstLetter(fieldName)} is required`
          )
          isRequired = true
        } else {
          this.showSuccess(fieldName)
        }
      })
      return isRequired
    },
    checkLength(formFieldName, min, max) {
      if (this[formFieldName].trim().length < min) {
        this.showError(
          formFieldName,
          `${this.capitalizeFirstLetter(
            formFieldName
          )} must be at least ${min} characters`
        )
      } else if (this[formFieldName].trim().length > max) {
        this.showError(
          formFieldName,
          `${this.capitalizeFirstLetter(
            formFieldName
          )} must be less than ${max} characters`
        )
      } else {
        this.showSuccess(formFieldName)
      }
    },
    checkEmail(email) {
      const re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      if (re.test(email.trim().toLowerCase())) {
        this.showSuccess('email')
      } else {
        this.showError('email', 'Email is not valid')
      }
    },
    checkPasswordMatch(password, password2) {
      if (password !== password2) {
        this.showError('password2', 'Passwords do not match')
      }
    },
    capitalizeFirstLetter(input) {
      return input.charAt(0).toUpperCase() + input.slice(1)
    },
    showError(formFieldName, message) {
      this[formFieldName + 'ErrMsg'] = message
      this[formFieldName + 'ErrClass'] = 'error'
    },
    showSuccess(formFieldName) {
      this[formFieldName + 'ErrMsg'] = ''
      this[formFieldName + 'ErrClass'] = 'success'
    },
  },
}
</script>

<style scoped>
.form-validator-body {
  --success-color: #2ecc71;
  --error-color: #e74c3c;

  background-color: #f9fafb;
  font-family: 'Open Sans', sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  margin: 0;
}

.container {
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
  width: 400px;
}

h2 {
  text-align: center;
  margin: 0 0 20px;
}

.form {
  padding: 30px 40px;
}

.form-control {
  margin-bottom: 10px;
  padding-bottom: 20px;
  position: relative;
}

.form-control label {
  color: #777;
  display: block;
  margin-bottom: 5px;
}

.form-control input {
  border: 2px solid #f0f0f0;
  border-radius: 4px;
  display: block;
  width: 100%;
  padding: 10px;
  font-size: 14px;
}

.form-control input:focus {
  outline: 0;
  border-color: #777;
}

.form-control.success input {
  border-color: var(--success-color);
}

.form-control.error input {
  border-color: var(--error-color);
}

.form-control small {
  color: var(--error-color);
  position: absolute;
  bottom: 0;
  left: 0;
  visibility: hidden;
}

.form-control.error small {
  visibility: visible;
}

.form button {
  cursor: pointer;
  background-color: #3498db;
  border: 2px solid #3498db;
  border-radius: 4px;
  color: #fff;
  display: block;
  font-size: 16px;
  padding: 10px;
  margin-top: 20px;
  width: 100%;
}
</style>