<template>
<v-app>
  <NavBar2/>
  <v-main>
    <v-card  width="550" id="loginCard">
      <v-card-title class="justify-center">Login to WeatherWetten!</v-card-title>
      <v-card-text>
        <v-text-field color="info" v-model="auth.email" label="E-Mail" outlined/>
        <v-text-field outlined
                      color="info"
                      v-model="auth.password"
                      label="Password"
                      :rules="validatePassword"
                      :type="showPassword ? 'text' : 'password'"
                      :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
                      @click:append="showPassword = !showPassword"/>
      </v-card-text>


      <v-card-actions class="justify-center">
        <v-btn id="loginButton" @click="login">Login</v-btn>
        <v-btn id="newHereButton" @click="routeToSignUp">New here?</v-btn>
      </v-card-actions>
      <v-card-actions class="justify-center">
        <v-btn id="forgotButton" @click="routeToForgotPassword">Forgot your password?</v-btn>
      </v-card-actions>
    </v-card>

    <v-snackbar timeout="10000" id="snackbar" v-model="showSnackbar" color="info">
      {{ userMsg }}
      <template v-slot:action="{ attrs }">
        <v-btn dark text v-bind="attrs" @click="showSnackbar = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </v-main>
</v-app>




</template>


<script>
import NavBar from "@/components/NavBar";
import SignUp from "@/pages/SignUp";
import forgotPassword from "@/pages/forgotPassword";

export default {
  data(){
    return {
      showPassword: false,
      showSnackbar: false,
      userMsg: "",

      auth: {
        email: "",
        password: ""
      },

      validatePassword: [
        (v) => !!v || "Password is required",
      ],

    }
  },

  name: "Login",

  components: {
    NavBar

  },
  methods:{
    routeToSignUp(){
      this.$router.push('SignUp')
    },

    login(){
      let that = this
      this.$fire.auth.signInWithEmailAndPassword(this.auth.email, this.auth.password)
      .catch(function (error) {
        switch (error.code) {
          case "auth/wrong-password":
            that.showSnackbar = true;
            that.userMsg = "You entered a wrong password";
            break;
          case "auth/user-not-found":
            that.showSnackbar = true;
            that.userMsg = "No user with the entered email address found";
            break;
          case "auth/user-disabled":
            that.showSnackbar = true;
            that.userMsg = "Your account has been disabled";
            break;
          default:
            that.showSnackbar = true;
            that.userMsg = error.message;
        }

      }).then((user) => {
        // that.$router.push('profile')
      })
    },


    routeToForgotPassword() {
      this.$router.push('forgotPassword')
    },


  }
}
</script>

<style scoped>


#loginCard{
  position: fixed;
  top: 35%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 5px;

}

#loginButton{
  color: forestgreen;
}

#newHereButton{
  color: forestgreen;
}

#forgotButton{
  color: orange;
}


</style>
