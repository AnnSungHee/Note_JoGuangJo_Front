<template>
  <v-container>
    <!--  <h2>굿즈 상품 등록</h2> -->
    <product-list-form :products="products" @addToCart="addToCart" />
    <!-- <button style="background-color: #FEE789; color: black; padding: 5px 10px; border: none; border-radius: 5px;"
      @click="navigateToRegister">
      상품 등록하기
    </button> -->
  </v-container>
</template>

<script>
import ProductListForm from "@/components/boards/product/ProductListForm.vue";
import { mapActions, mapState } from "vuex";

const productModule = 'productModule'

export default {
  components: { ProductListForm },
  name: "ProductListView",
  computed: {
    ...mapState(productModule, ["products"]),
    ...mapState("account", ["isAuthenticated"])
  },
  mounted() {
    this.requestProductListToSpring();
  },
  methods: {
    ...mapActions(productModule, ["requestProductListToSpring"]),
    ...mapActions("cartModule", ["requestRegisterCartToSpring"]),
    addToCart(payload) {
      if (this.isAuthenticated === true) {
        const { productId } = payload
        const memberId = JSON.parse(localStorage.getItem("userInfo")).id;
        let count = 1; // 수량은 현재 임시용
        this.requestRegisterCartToSpring({ memberId, productId, count })
        let goToCartMessage = confirm("장바구니로 이동하시겠습니까?")
        if (goToCartMessage) {
          this.$router.push({ name: 'CartListView' });
        }
      } else {
        this.$router.push({ name: 'SignInView' })
      }
    },
    navigateToRegister() {
      if (this.isAuthenticated) {
        this.$router.push({ name: "ProductRegisterView" });
      } else {
        this.$router.push({ name: "SignInView" });
      }
    },
  },
};
</script>

<style scoped>
.header-form {
  margin-left: -20px;
}

.h2 {
  text-align: center;
}
</style>>
