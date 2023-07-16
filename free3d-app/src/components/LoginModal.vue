<template>
  <div id="login-root">
    <div class="notifier" v-show="isNotifierEnabled">{{ notifier_message }}</div>

    <div class="login-header">
    </div>
    <div class="login-main">
      <div class="dropdown">
        <div class="triangle"></div>

        <form v-on:submit.prevent>
          <div class="input-group">
            <label>Email</label>
            <br>
            <input class="login-input text" type="text" v-model="input_login_email">
            <br>

            <label>Password</label>
            <br>
            <input class="login-input text" type="password" v-model="input_login_password">
            <br>
          </div>
          <div class="button-group">
            <div class="login-remember-me">
              <button class="login-input submit-button" v-on:click="submitLogin()" >
              Login
              </button>

              <div class="remember">
                <input class="login-input remember-me-checkbox" type="checkbox" checked>
                <label>Remember me</label>
              </div>

            </div>

            <div class="other-login">
              <p>or login with</p>
              <div class="other-login-button-group">
                <div class="google-button">
                  <div class="google-icon-wrapper">
                    <img class="google-icon"
                      src="https://upload.wikimedia.org/wikipedia/commons/5/53/Google_%22G%22_Logo.svg" />
                  </div>
                  <p class="btn-text"><b>Google</b></p>
                </div>
                <div class="facebook-button">
                  <div class="facebook-icon-wrapper">
                    <img class="facebook-icon"
                      src="https://upload.wikimedia.org/wikipedia/commons/5/53/Google_%22G%22_Logo.svg" />
                  </div>
                  <p class="btn-text"><b>Facebook</b></p>
                </div>
              </div>
            </div>
          </div>
          <br>
        </form>


        <p class="forgot">
          <a href="reset-password.html">Forgot password ?</a>
        </p>

      </div>
    </div>
    <div class="login-footer">
    </div>

  </div>
</template>

<script>

const INVALID_INPUT_ENUM = Object.freeze({
  empty_input_login: Symbol("empty_input_login"),
  not_an_email_input_login: Symbol("not_an_email_input_login"),
  empty_input_password: Symbol("empty_input_password"),
  fine: Symbol("fine"),
})

export default {
  name: 'LoginModal',
  methods: {
    submitLogin() {
      let [isPassed, invalidInputType] = this.validate();
      if (isPassed) {
        //do nothing, cuz no backend to accept POST message
        return;
      }

      this.showNotifierMessage(invalidInputType);

    },
    validate() {
      let isPassed = true;
      let invalidInputType = INVALID_INPUT_ENUM.fine;

      if (this.input_login_email == "") {
        isPassed = false;
        invalidInputType = INVALID_INPUT_ENUM.empty_input_login;

        return [isPassed, invalidInputType];
      }

      if (this.input_login_password == "") {
        isPassed = false;
        invalidInputType = INVALID_INPUT_ENUM.empty_input_password;

        return [isPassed, invalidInputType];
      }

      if (this.isAnEmail(this.input_login_email) == false) {
        isPassed = false;
        invalidInputType = INVALID_INPUT_ENUM.not_an_email_input_login;

        return [isPassed, invalidInputType];
      }

      return [isPassed, invalidInputType];
    },

    isAnEmail(input) {
      if (!input)
        return false;

      if (this.isString(input) == false)
        return false;

      let input_string = String(input);

      let indexOfEmailSymbol = input_string.lastIndexOf("@");


      let indexOfDot = input_string.lastIndexOf(".");

      if (indexOfDot < 0
        || indexOfDot > input_string.length)
        return false;


      if (indexOfEmailSymbol >= indexOfDot)
        return false;

      if (input_string.substring(indexOfDot).length < 2)
        return false;
      return true;
    },

    isString(target) {
      return (typeof target === 'string' || target instanceof String)
    },

    showNotifierMessage(invalidInputType) {
      this.notifier_show_timer = 4;
      switch (invalidInputType) {
        case INVALID_INPUT_ENUM.empty_input_login:

          this.notifier_message = "Please fill out the Email field";
          this.isNotifierEnabled = true;
          break;

        case INVALID_INPUT_ENUM.not_an_email_input_login:

          this.notifier_message = "Please enter a valid the email address";
          this.isNotifierEnabled = true;
          break;

        case INVALID_INPUT_ENUM.empty_input_password:

          this.notifier_message = "Please fill out the Password field";
          this.isNotifierEnabled = true;
          break;

        case INVALID_INPUT_ENUM.fine:
          break;

        default:
          console.error("Missing INVALID_INPUT_ENUM config for new case: " + invalidInputType);
      }
      console.log("Show timer for " + this.notifier_show_timer);

      clearTimeout(this.currentTimeout);
      this.currentTimeout = setTimeout(this.hideNotifier, this.notifier_show_timer * 1000 );
    },

    hideNotifier() {
      this.isNotifierEnabled = false;
      this.notifier_message = "";
    },

    close() {
      this.$emit('close');
    },
  },
  props: {
    msg: String
  },
  data: function () {
    return {
      input_login_email: "",
      input_login_password: "",

      notifier_message: "",
      notifier_show_timer: 0,
      isNotifierEnabled: false,

      currentTimeout:"",
    }
  },

  // watch: {

  //   notifier_show_timer: {
  //     handler(value) {

  //       if (value > 0) {
  //         setTimeout(() => {
  //           this.notifier_show_timer--;
            
  //           console.log("Timer remain " + this.notifier_show_timer);
  //           if (this.notifier_show_timer <= 0
  //             && this.isNotifierEnabled == true) {
  //             this.hideNotifier();
  //           }

  //         }, 1000);
  //       }

  //     },
  //     immediate: true // This ensures the watcher is triggered upon creation
  //   }
  // }
}
</script>


<style scoped>
@import '../assets/css/login.css';
</style>
