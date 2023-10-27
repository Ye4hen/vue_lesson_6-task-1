<template>
  <div>
    {{ title }}
    <div>
      <label>
        <input :class="checkColorName" type="text" v-model="userNameValue" />
      </label>
      <label>
        <input :class="checkColorAge" type="number" v-model="userAgeValue" />
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserInfoManager",
  props: {
    title: {
      type: String,
    },
    userName: { type: String },
    userNameModifiers: { default: () => ({}) },
    userAge: { type: Number },
    userAgeModifiers: { default: () => ({}) },
  },
  data() {
    return {
      checkColorName: null,
      checkColorAge: null,
    };
  },
  computed: {
    userNameValue: {
      get() {
        return this.userName;
      },
      set(val) {
        if (this.userNameModifiers.existence) {
          if (val) this.checkColorName = null;
          else this.checkColorName = "error-color";
        }
        this.$emit("update:userName", val, this.checkColorName);
      },
    },
    userAgeValue: {
      get() {
        return this.userAge;
      },
      set(val) {
        if (this.userAgeModifiers.ageVerification) {
          if (val) {
            if (val < 18) this.checkColorAge = "error-color";
            else this.checkColorAge = "valid-color";
          } else this.checkColorAge = null;
        }

        this.$emit("update:userAge", val, this.checkColorAge);
      },
    },
  },
};
</script>

<style lang="css" scoped>
.error-color {
  background-color: red;
}
.valid-color {
  background-color: green;
}
</style>
