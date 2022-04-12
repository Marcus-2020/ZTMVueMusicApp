<template>
  <div class="text-white text-center font-bold p-5 mb-4"
       v-if="show_alert" :class="alert_variant">
    {{ alert_msg }}
  </div>
  <vee-form
    :validation-schema="registerSchema" @submit="register"
    :initial-values="userData">
    <!-- Name -->
    <div class="mb-3">
      <label for="register-name" class="inline-block mb-2">
        Name
      </label>
      <vee-field id="register-name" type="text" name="name"
         class="block w-full py-1.5 px-3 text-gray-800 border border-gray-300 transition
            duration-500 focus:outline-none focus:border-black rounded"
         placeholder="Enter Name" />
      <ErrorMessage class="text-red-600" name="name" />
    </div>
    <!-- Email -->
    <div class="mb-3">
      <label for="register-email" class="inline-block mb-2">
        Email
      </label>
      <vee-field id="register-email" type="email" name="email"
         class="block w-full py-1.5 px-3 text-gray-800 border border-gray-300 transition
            duration-500 focus:outline-none focus:border-black rounded"
         placeholder="Enter Email"/>
      <ErrorMessage class="text-red-600" name="email" />
    </div>
    <!-- Age -->
    <div class="mb-3">
      <label for="register-age" class="inline-block mb-2">
        Age
      </label>
      <vee-field id="register-age" type="number" name="age"
         class="block w-full py-1.5 px-3 text-gray-800 border border-gray-300 transition
            duration-500 focus:outline-none focus:border-black rounded"/>
      <ErrorMessage class="text-red-600" name="age" />
    </div>
    <!-- Password -->
    <div class="mb-3">
      <label for="register-password" class="inline-block mb-2">
        Password
      </label>
      <vee-field name="password" :bails="false" v-slot="{ field, errors }">
        <input id="register-password" type="password"
           class="block w-full py-1.5 px-3 text-gray-800 border border-gray-300 transition
              duration-500 focus:outline-none focus:border-black rounded"
           placeholder="Password" v-bind="field" />
        <div class="text-red-600" v-for="error in errors" :key="error">
          {{ error }}
        </div>
      </vee-field>
    </div>
    <!-- Confirm Password -->
    <div class="mb-3">
      <label for="register-confirm-password" class="inline-block mb-2">
        Confirm Password
      </label>
      <vee-field id="register-confirm-password" type="password" name="confirm_password"
         class="block w-full py-1.5 px-3 text-gray-800 border border-gray-300 transition
            duration-500 focus:outline-none focus:border-black rounded"
         placeholder="Confirm Password"/>
      <ErrorMessage class="text-red-600" name="confirm_password" />
    </div>
    <!-- Country -->
    <div class="mb-3">
      <label for="register-country" class="inline-block mb-2">
        Country
      </label>
      <vee-field as="select" id="register-country" name="country"
         class="block w-full py-1.5 px-3 text-gray-800 border border-gray-300 transition
            duration-500 focus:outline-none focus:border-black rounded">
        <option value="USA">USA</option>
        <option value="Mexico">Mexico</option>
        <option value="Germany">Germany</option>
        <option value="Antartica">Antartica</option>
      </vee-field>
      <ErrorMessage class="text-red-600" name="country" />
    </div>
    <!-- TOS -->
    <div class="mb-3 pl-6">
      <vee-field id="register-terms-of-service" name="tos" value="1"
                 type="checkbox"
                 class="w-4 h-4 float-left -ml-6 mt-1 rounded block"/>
      <label for="register-terms-of-service" class="inline-block">
        Accept terms of service
      </label>
      <ErrorMessage class="text-red-600 block" name="tos" />
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
  name: 'AppRegisterForm',
  data() {
    return {
      userData: {
        country: 'USA',
      },
      registerSchema: {
        name: 'required|min:3|max:100|alpha_spaces',
        email: 'required|min:3|max:100|email',
        age: 'required|min_value:18|max_value:100',
        password: 'required|min:3|max:100',
        confirm_password: 'required|password_mismatch:@password',
        country: 'required|country_excluded:Antartica,',
        tos: 'tos',
      },
      in_submission: false,
      show_alert: false,
      alert_variant: 'bg-blue-500',
      alert_msg: 'Please wait! Your account is being created.',
    };
  },
  methods: {
    register(values) {
      this.show_alert = true;
      this.in_submission = true;
      this.alert_variant = 'bg-blue-500';
      this.alert_msg = 'Please wait! Your account is being created.';

      setTimeout(() => {
        this.alert_variant = 'bg-green-500';
        this.alert_msg = 'Success! Your account successfully created.';
        console.log(values);
      }, 2000);
    },
  },
};
</script>
