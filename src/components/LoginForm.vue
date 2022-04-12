<template>
  <div class="text-white text-center font-bold p-5 mb-4"
       v-if="show_alert" :class="alert_variant">
    {{ alert_msg }}
  </div>
  <vee-form
    :validation-schema="loginSchema" @submit="login">
    <!-- Email -->
    <div class="mb-3">
      <label for="login-email" class="inline-block mb-2">
        Email
      </label>
      <vee-field id="login-email" type="email" name="email"
        class="block w-full py-1.5 px-3 text-gray-800 border border-gray-300 transition
          duration-500 focus:outline-none focus:border-black rounded"
        placeholder="Enter Email"/>
      <ErrorMessage class="text-red-600" name="email" />
    </div>
    <!-- Password -->
    <div class="mb-3">
      <label for="login-password" class="inline-block mb-2">
        Password
      </label>
      <vee-field name="password" id="login-password" type="password"
         class="block w-full py-1.5 px-3 text-gray-800 border border-gray-300 transition
            duration-500 focus:outline-none focus:border-black rounded"
         placeholder="Password" />
      <ErrorMessage class="text-red-600" name="password" />
    </div>
    <button type="submit" :disabled="in_submission"
      class="block w-full bg-purple-600 text-white py-1.5 px-3 rounded transition
          hover:bg-purple-700">
      Submit
    </button>
  </vee-form>
</template>

<script>
export default {
  name: 'AppLoginForm',
  data() {
    return {
      loginSchema: {
        email: 'required|min:3|max:100|email',
        password: 'required|min:3|max:100',
      },
      in_submission: false,
      show_alert: false,
      alert_variant: 'bg-blue-500',
      alert_msg: 'Please wait! We are logging you in.',
    };
  },
  methods: {
    login(values) {
      this.show_alert = true;
      this.in_submission = true;
      this.alert_variant = 'bg-blue-500';
      this.alert_msg = 'Please wait! You are being logged in.';

      setTimeout(() => {
        this.alert_variant = 'bg-green-500';
        this.alert_msg = 'Success! Your has successfully logged in.';
        console.log(values);
      }, 2000);
    },
  },
};
</script>
