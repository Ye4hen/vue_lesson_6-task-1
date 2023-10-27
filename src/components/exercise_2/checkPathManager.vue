<template>
  <div>
    <label>
      {{ title }}
      <input :class="checkColor" type="text" v-model="path" />
    </label>
  </div>
</template>

<script>
export default {
  name: "checkPathManager",
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
      checkColor: null,
    };
  },
  computed: {
    path: {
      get() {
        return this.modelValue;
      },
      set(val) {
        if (this.modelModifiers.checkPath) {
          const jsExtansion = /\.js$/i;
          if (val) {
            if (!jsExtansion.test(val)) {
              this.checkColor = "wrong-url-color";
            } else {
              this.checkColor = null;
            }
          } else {
            this.checkColor = null;
          }
        }

        this.$emit("update:modelValue", val);
      },
    },
  },
};
</script>

<style lang="css" scoped>
.wrong-url-color {
  background-color: red;
}
</style>
