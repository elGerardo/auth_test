<template>
  <b-container>
    <b-form @submit.prevent="signup()">
      <b-input placeholder="email" type="text" v-model="form.email" />
      <b-input placeholder="password" type="password" v-model="form.password" />
      <b-button type="submit">Register</b-button>
    </b-form>
  </b-container>
</template>
<script>
export default {
  data() {
    return {
      form: {
        email:'',
        password:'',
      },
    };
  },

  methods: {
    async signup() {
        console.log("submiting...");

        await this.$fire.auth.createUserWithEmailAndPassword(this.form.email, this.form.password)
        .then(userCredential => {
            console.log("user created...")
            this.$fire.auth.currentUser.sendEmailVerification().then(response => {
                console.log("email sent...");
            }).catch(e => {
                console.log("error", e);
            })
        })
    },
  },
};
</script>
