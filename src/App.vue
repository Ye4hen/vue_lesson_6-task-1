<template>
  <user-age-manager title="Enter your age" v-model.check.setColor="userAge" />
  <hr />
  <check-path-manager title="Enter the path" v-model.checkPath="filePath" />
  <hr />
  <email-manager title="Enter your email" v-model.check="userEmail" />
  <hr />
  <user-info-manager
    title="Enter your info"
    v-model:userName.existence="userInfoName"
    v-model:userAge.ageVerification="userInfoAge"
  />
</template>

<script>
import UserInfoManager from "./components/exerciese_4/UserInfoManager.vue";
import UserAgeManager from "./components/exercise_1/userAgeManager.vue";
import checkPathManager from "./components/exercise_2/checkPathManager.vue";
import EmailManager from "./components/exercise_3/EmailManager.vue";

export default {
  name: "App",
  components: {
    UserAgeManager,
    checkPathManager,
    EmailManager,
    UserInfoManager,
  },
  data() {
    return {
      userAge: null,
      filePath: null,
      userEmail: null,
      userInfoAge: null,
      userInfoName: null,
    };
  },
  methods: {},
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
