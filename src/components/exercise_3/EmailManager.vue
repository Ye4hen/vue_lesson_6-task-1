<template>
  <div>
    {{ title }}
    <label>
      <input
        :class="emailColor"
        v-model="email"
        type="email"
        @blur="updateEmail(email)"
      />
    </label>
    <button @click="checkEmail">Check Email</button>
    <div :class="errorMessageStyle" v-if="errorMessage">{{ errorMessage }}</div>
  </div>
</template>

<script>
import { emailsRegister } from "@/constants/exercise_3/emailsRegister.js";
export default {
  name: "EmailManager",
  props: {
    title: {
      type: String,
      required: true,
    },
    modelValue: {
      type: String,
    },
    modelModifiers: {
      default: () => ({}),
    },
  },
  data() {
    return {
      emailColor: null,
      emailTimeout: null,
      errorMessage: null,
      errorMessageStyle: null,
    };
  },
  computed: {
    email: {
      get() {
        return this.modelValue;
      },
      set(val) {
        if (this.modelModifiers.check) {
          const findEmail = emailsRegister.find((user) => {
            return user.email === this.email;
          });

          if (!findEmail) {
            this.emailColor = "wrong-email-color";
          } else {
            this.emailColor = "right-email-color"; // Set the class to "right-email-color" for correct emails
          }
        }
        this.$emit("update:modelValue", val);
      },
    },
  },
  methods: {
    updateEmail(value) {
      if (!value.endsWith("@inv.mn.edu")) {
        value += "@inv.mn.edu";
      }
      this.$emit("update:modelValue", value);
    },
    checkEmail() {
      const findEmail = emailsRegister.find((user) => {
        return user.email === this.email;
      });
      if (findEmail) {
        this.errorMessage = "Welcome aboard, sir!";
        this.errorMessageStyle = "right-message-style";
        this.emailColor = null;
      } else {
        this.errorMessage = "WRONG!";
        this.errorMessageStyle = "wrong-message-style";
      }
    },
  },
};
</script>

<style lang="css" scoped>
.wrong-email-color {
  background-color: red;
}
.right-email-color {
  background-color: green;
}
.right-message-style {
  color: green;
  font-size: 18px;
}
.wrong-message-style {
  color: red;
  font-size: 25px;
}
</style>
