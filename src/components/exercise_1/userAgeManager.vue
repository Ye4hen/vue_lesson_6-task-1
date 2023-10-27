<template>
  <label>
    {{ title }}
    <input :class="ageColor" type="number" v-model="age" />
  </label>
  <div>{{ errorMessage }}</div>
</template>

<script>
export default {
  name: "userAgeManager",

  props: {
    title: {
      type: String,
      required: true,
    },
    modelValue: {
      type: Number,
    },
    modelModifiers: {
      default: () => ({}),
    },
  },
  data() {
    return {
      errorMessage: null,
      ageColor: null,
    };
  },
  computed: {
    age: {
      get() {
        return this.modelValue;
      },
      set(val) {
        val = Math.min(151, Math.max(0, val));
        if (this.modelModifiers.check) {
          if (val > 150) {
            this.errorMessage = "вік не може бути більшим за 150";
            val = null;
          } else if (val < 0) {
            this.errorMessage = "вік не може бути меньшим за 0";
            val = null;
          } else {
            this.errorMessage = null;
          }
        }
        if (this.modelModifiers.setColor) {
          if (val) {
            if (val < 10) this.ageColor = "young-user-color";
            else if (val <= 21) this.ageColor = "teenager-user-color";
            else if (val > 21) this.ageColor = "old-user-color";
          } else this.ageColor = null;
        }
        this.$emit("update:modelValue", val, this.ageColor);
      },
    },
  },
};
</script>

<style lang="css">
.young-user-color {
  background-color: green;
}
.teenager-user-color {
  background-color: yellow;
}
.old-user-color {
  background-color: orange;
}
</style>
