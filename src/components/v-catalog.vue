<template>
  <div class="v-catalog">
    <router-link :to="{ name: 'cart', params: { cart_data: CART } }">
      <div class="v-catalog__link_to_cart">
        Cart: {{ CART.length }}
      </div></router-link
    >
    <h1>Каталог</h1>
    <v-select
      :categories="categories"
      :selected="selected"
      @select="sortByCategories"
    />
    <div class="v-catalog_list">
      <v-catalog-item
        v-for="product of filteredProducts"
        :key="product.article"
        :product="product"
        @addToCart="addToCart"
      />
    </div>
  </div>
</template>

<script>
import vCatalogItem from "./v-catalog-item.vue";
import { mapActions, mapGetters } from "vuex";
import vSelect from "./v-select.vue";

export default {
  name: "v-catalog",
  components: {
    vCatalogItem,
    vSelect,
  },
  props: {},
  data() {
    return {
      categories: [
        { name: "Все", value: "ALL" },
        { name: "Юбилеиная", value: "ю" },
        { name: "Обычная", value: "о" },
      ],
      selected: "Все",
      sortedProducts: [],
    };
  },
  computed: {
    ...mapGetters(["PRODUCTS", "CART"]),
    filteredProducts() {
      if (this.sortedProducts.length) {
        return this.sortedProducts;
      } else {
        return this.PRODUCTS;
      }
    },
  },
  methods: {
    ...mapActions(["GET_PRODUCTS_FROM_API", "ADD_TO_CART"]),
    addToCart(data) {
      this.ADD_TO_CART(data);
    },
    sortByCategories(category) {
      this.sortedProducts = [];
      let vm = this;
      this.PRODUCTS.map((item) => {
        if (item.category === category.name) {
          vm.sortedProducts.push(item);
        }
      });
      this.selected =category.name
    },
  },
  watch: {},
  mounted() {
    this.GET_PRODUCTS_FROM_API();
  },
};
</script>

<style lang="scss">
.v-catalog {
  &_list {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
  }
  &__link_to_cart {
    position: absolute;
    top: 10px;
    right: 10px;
    padding: $padding * 2;
    border: 1px solid #aeaeae;
  }
}
</style>
