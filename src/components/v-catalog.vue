<template>
  <div class="v-catalog">
    <router-link :to="{ name: 'cart', params: { cart_data: CART } }">
      <div class="v-catalog__link_to_cart">
        Cart: {{ CART.length }}
      </div></router-link
    >
    <h1>Каталог</h1>
    <div class="filters">
      <v-select
        :categories="categories"
        :selected="selected"
        @select="sortByCategories"
        :isExpanded="IS_DESKTOP"
      />
      <div class="range-slider">
        <input
          type="range"
          min="0"
          max="10000"
          step="100"
          v-model.number="minPrice"
          @change="setRangesSlider"
        />
        <input
          type="range"
          min="0"
          max="10000"
          step="100"
          v-model.number="maxPrise"
          @change="setRangesSlider"
        />
      </div>
      <div class="range-values">
        <p>min: {{ minPrice }}</p>
        <p>max: {{ maxPrise }}</p>
      </div>
    </div>

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
      minPrice: 0,
      maxPrise: 10000,
    };
  },
  computed: {
    ...mapGetters(["PRODUCTS", "CART", "IS_MOBILE", "IS_DESKTOP"]),
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
    setRangesSlider() {
      if (this.minPrice > this.maxPrise) {
        let temp = this.maxPrise;
        this.maxPrise = this.minPrice;
        this.minPrice = temp;
      }
      this.sortByCategories();
    },

    sortByCategories(category) {
      let vm = this;
      this.sortedProducts = [...this.PRODUCTS];
      this.sortedProducts = this.sortedProducts.filter((item) => {
        return item.price >= vm.minPrice && item.price <= vm.maxPrise;
      });
      if (category) {
        this.sortedProducts = this.sortedProducts.filter((e) => {
          vm.selected === category.name;
          return e.category === category.name;
        });
      }
      // ----------------
      // this.sortedProducts = [];
      // let vm = this;
      // this.PRODUCTS.map((item) => {
      //   if (item.category === category.name) {
      //     vm.sortedProducts.push(item);
      //   }
      // });
      // this.selected = category.name;
      // ----------------
    },
  },
  watch: {},
  mounted() {
    this.GET_PRODUCTS_FROM_API().then((response) => {
      if (response.data) {
        this.sortByCategories();
      }
    });
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
.filters {
  display: flex;
  justify-content: space-between;
  align-items: 0;
}

.range-slider {
  width: 200px;
  margin: auto 16px;
  text-align: center;
  position: relative;
}

.range-slider svg,
.range-slider input[type="range"] {
  position: absolute;
  left: 0;
  bottom: 0;
}

input[type="range"]::-webkit-slider-thumb {
  z-index: 2;
  position: relative;
  top: 2px;
  margin-top: -7px;
}
</style>
