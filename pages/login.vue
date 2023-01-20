<template>
  <b-container>
    <b-form @submit.prevent="submit()">
        <b-input placeholder="email" type="text" v-model="form.email" />
      <b-input placeholder="password" type="password" v-model="form.password" />
      <b-button type="submit">Login</b-button>
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
    async submit() {
        console.log("submiting...");

        await this.$fire.auth.signInWithEmailAndPassword(this.form.email, this.form.password)
        .then(credentials => {
            console.log("loged success...");
            console.log(credentials);
        }).catch(error => {
            console.log("error login", error);
        })
    },
  },
};
</script>
