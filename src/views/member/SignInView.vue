<template>
  <div>
    <login-form @submit="onSubmit"></login-form>
  </div>
</template>
  
<script>

import { mapActions, mapState } from "vuex";
import Vue from "vue";
import cookies from "vue-cookies";
import LoginForm from "@/components/member/SignInForm.vue";

Vue.use(cookies);

export default {
  name: "SignInView",
  components: {
    LoginForm,
  },
  data() {
    return {
      isLogin: false,
    };
  },
  computed: {
    ...mapState("account", ["isAuthenticated"]),
  },
  mounted() {
  if (this.isAuthenticated != false) {
    this.isLogin = true;
  } else {
    this.isLogin = false;
  }
},
methods: {
  ...mapActions("account", ["login"]),
  onSubmit(payload) {
    if (!this.isLogin) {
      const { email, password } = payload;
      this.login({ email, password })
        .then((userData) => {
          if (userData) {
            alert("로그인 성공!");
            cookies.set("user", userData, 3600);
            localStorage.setItem("userInfo", JSON.stringify(userData));
            this.isLogin = true;    
            if (this.$route.path !== "/") {
              this.$router.push("/");
            }
          }
        })
        .catch((error) => {
          if (error.response && error.response.data) {
            alert("로그인 정보가 잘 못 되었습니다.");
          } else {
            alert("An unknown error occurred.");
          }
        });
    } else {
      alert("이미 로그인이 되어 있습니다!");
    }
  },
},

};

</script>

<style scoped>

</style>