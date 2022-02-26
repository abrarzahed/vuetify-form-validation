<template>
  <v-app>
    <div class="form-wrapper">
      <v-card width="400" class="pa-6">
        <h4 class="text-h4 text-center font-weight-bold">Register Now</h4>

        <v-form @submit.prevent="handleSubmit" ref="form" v-model="valid">
          <div class="form-group">
            <v-text-field
              v-model="formInputs.name"
              :rules="nameRules"
              append-icon="mdi-account"
              formInputs.v-model="Username"
              :counter="10"
              label="Name"
              placeholder="Enter Username"
              required
            ></v-text-field>
          </div>

          <div class="from-group">
            <v-text-field
              v-model="formInputs.email"
              :rules="emailRules"
              append-icon="mdi-email"
              formInputs.v-model="email"
              label="E-mail"
              placeholder="Enter Email"
              required
            ></v-text-field>
          </div>
          <div class="form-group">
            <v-text-field
              v-model="formInputs.password"
              :rules="passwordRules"
              :append-icon="showPass1 ? 'mdi-eye' : 'mdi-eye-off'"
              formInputs.v-model="password"
              label="Password"
              placeholder="Enter Password"
              required
              :type="showPass1 ? 'text' : 'password'"
              @click:append="showPass1 = !showPass1"
            ></v-text-field>
          </div>

          <v-btn
            :disabled="!valid"
            type="submit"
            block
            color="success"
            class="mt-5"
          >
            Submit
          </v-btn>
        </v-form>
      </v-card>
      <!-- <v-card v-if="showData" width="400" class=""> -->

      <v-alert
        class="pa-6 my-10 data"
        dense
        text
        type="success"
        :class="{ 'show-data': showData }"
      >
        <p><strong>Username: </strong>{{ formInputs.name }}</p>
        <p><strong>Email: </strong>{{ formInputs.email }}</p>
        <h4>Successfully Registered</h4>
        <v-btn depressed text color="error" class="mt-5" @click="closeData"
          >Close</v-btn
        >
      </v-alert>
      <!-- </v-card> -->
    </div>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    showData: false,
    valid: true,
    showPass1: false,
    formInputs: {
      name: "",
      email: "",
      password: "",
      password2: "",
    },
    nameRules: [
      (v) => !!v || "Name is required",
      (v) => (v && v.length <= 10) || "Name must be less than 6 characters",
    ],
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
    ],
    passwordRules: [
      (v) => !!v || "Password is required",
      (v) => (v && v.length <= 10) || "Password must be less than 8 characters",
    ],
  }),

  methods: {
    handleSubmit() {
      // this.$refs.form.validate();
      this.showData = true;
    },
    closeData() {
      this.$refs.form.reset();
      this.showData = false;
    },
  },
};
</script>
<style lang="scss">
.form-wrapper {
  background: #eee;
  display: grid;
  place-content: center;
  min-height: 100%;
}
.data {
  opacity: 0;
  transition: opacity 0.5s ease-in;
}
.show-data.data {
  opacity: 1;
}
</style>
