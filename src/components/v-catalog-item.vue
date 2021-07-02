<template>
  <div class="v-catalog-item">
    <v-popup v-if="isInfoPopupVisible" 
    :popupTitle="product.name"
    rightBtnTitle="Add to cart" @closePopup="closeInfoPopup"
    @rightBtnAction="addToCart"
    >
      <img
        class="v-catalog-item_image"
        :src="require(`../assets/images/${product.image}`)"
        alt="img"
      />
      <div>
        <p class="v-catalog-item__name">{{ product.name }}</p>
        <p class="v-catalog-item__price">Price: {{ product.price }} руб.</p>
        <p class="v-catalog-item__price">Price: {{ product.category }}</p>
      </div>
    </v-popup>
    <img
      class="v-catalog-item_image"
      :src="require(`../assets/images/${product.image}`)"
      alt="img"
    />
    <p class="v-catalog-item__name">{{ product.name }}</p>
    <p class="v-catalog-item__price">Price: {{ product.price }} руб.</p>
    <button class="v-catalog-item__show-info" @click="showPopupInfo">
      Показать информацию
    </button>

    <button class="v-catalog-item__add_to_cart_btn btn" @click="addToCart">
      Add to card
    </button>
  </div>
</template>

<script>
import vPopup from "../components/popup/v-popup.vue";

export default {
  name: "v-catalog-item",
  components: {
    vPopup,
  },
  props: {
    product: {
      type: Object,

      default() {
        return {};
      },
    },
  },
  data() {
    return {
      isInfoPopupVisible: false,
    };
  },
  computed: {},
  methods: {
    addToCart() {
      this.$emit("addToCart", this.product);
    },
    closeInfoPopup() {
      this.isInfoPopupVisible = false;
    },
    showPopupInfo() {
      this.isInfoPopupVisible = true;
    },
  },
  watch: {},
  mounted() {},
};
</script>

<style lang="scss">
.v-catalog-item {
  flex-basis: 25%;
  box-shadow: 0 0 8px 0 #e8e8e8;
  padding: $padding * 2;
  margin-bottom: $margin * 2;
  text-align: center;
  &_image {
    width: 100px;
  }
}
</style>
