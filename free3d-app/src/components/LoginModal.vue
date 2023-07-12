<template>
  <div id="login-root">
    <div class="login-header">
    </div>
    <div class="login-main">
      <div class="dropdown">
        <div class="triangle"></div>

        <form>
          <div class="input-group">
            <label>Email</label>
            <br>
            <input class="login-input" type="text">
            <br>

            <label>Password</label>
            <br>
            <input class="login-input" type="text">
            <br>
          </div>
          <div class="button-group">
            <div class="login-remember-me">
              <input class="login-input submit-button" type="submit" value="Login">

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
export default {
  name: 'LoginModal',
  methods: {
    close() {
      this.$emit('close');
    },
  },
  props: {
    msg: String
  }
}
</script>


<style scoped>
@import '../assets/css/login.css';
</style>
