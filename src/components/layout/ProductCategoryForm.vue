<template>
  <div class="category-container">
    <v-divider></v-divider>
    <h2 class="title">카테고리</h2>
    <v-list dense>
      <v-list-item-group color="primary" class="category123" text-align="center;">
        <v-list-item v-for="(category, i) in categories" :key="i" @click="selectedCategory = category">
          <v-list-item-content>
            <v-list-item-title>{{ category }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
      <v-divider></v-divider>
      <v-list-item-group color="primary" class="category456" text-align="center;">
        <v-list-item v-for="(category, i) in additionalCategories" :key="i" @click="selectedCategory = category">
          <v-list-item-content>
            <v-list-item-title>{{ category }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "ProductCategoryForm",
  data() {
    return {
      selectedCategory: "전체",
      categories: ["전체", "문구류", "도서", "굿즈"],
      additionalCategories: [],
    };
  },
};
</script>

<style scoped>
.category-container {
  margin-bottom: 70px;
  margin-left: 40px;
  width: 100%;
}

.title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 10px;
  margin-left: -8px;
  padding-left: 20px;
}

.category123, .category456 {
  align-items: center;
}

.v-list-item:hover {
  background-color: #FEE789;
}
</style>
