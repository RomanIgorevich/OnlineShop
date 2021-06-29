<template>
  <div class="v-catalog-item">
    <img class="v-catalog-item_image" :src="require(`../assets/images/${product.image}`)" alt="img" />
    <p class="v-catalog-item__name">{{ product.name }}</p>
    <p class="v-catalog-item__price">Price: {{ product.price }} руб.</p>
    <button
      class="v-catalog-item__add_to_cart_btn btn"
     
    >
      Add to card
    </button>
  </div>
</template>

<script>
export default {
  name: "v-catalog-item",
  components: {},
  props: {
    product: {
      type: Object,

      default() {
        return {};
      },
    },
  },
  data() {
    return {};
  },
  computed: {},
  methods: {},
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
