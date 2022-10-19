<template>
  <v-form>
    <v-container>
      <v-row>

        <v-col
          cols="12"
        >
          <v-text-field
            v-model="email.value"
            label="E-mail"
            :rules="emailErrors"
            @change="$v.$touch"
            @input="$v.$touch"
            @blur="$v.$touch"
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"
        >
          <v-text-field
            v-model="password.value"
            :rules="passwordErrors"
            label="Password"
            @change="$v.$touch"
            @input="$v.$touch"
            @blur="$v.$touch"
          ></v-text-field>
        </v-col>

        <v-btn
          :disabled="this.$v.$invalid"
          color="success"
          class="mr-4"
          @click="loginAction"
        >
          Validate
        </v-btn>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
import { email, minLength, required } from "vuelidate/lib/validators";
import { validationMixin } from "vuelidate";

export default {
  name: 'LoginForm',
  mixins: [validationMixin],
  data: () => ({
    password: {
      value: '',
      validations: {
        minLength: 'too short',
        required: "password is required!"
      }
    },
    email: {
      value: '',
      validations: {
        required: "email is required!",
        email: 'should be a valid email',
      }
    }
  }),
  computed: {
    emailErrors () {
      return this.getValidationErrorsByInputName('email', this.email.value)
    },
    passwordErrors () {
      return this.getValidationErrorsByInputName('password', this.password.value )
    }
  },
  methods: {
    loginAction () {
      this.$v.$touch()
      if (!this.$v.$invalid) this.$emit('success')
    },
    getValidationErrorsByInputName (name) {
      const result = []
      const validations = Object.keys(this.$v[name].$model.validations)
      for (let i = 0; i < validations.length; i++) {
        const validationName = validations[i]
        const isValidationError = !this.$v[name].value[validationName]
        if (isValidationError) result.push(this[name].validations[validationName])
      }
      return result
    }
  },
  validations () {
    return {
      password: {
        value: {
          minLength: minLength(6),
          required
        }
      },
      email: {
        value: {
          required,
          email
        }
      }
    }
  }
};
</script>
