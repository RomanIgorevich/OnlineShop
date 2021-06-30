<template>
  <div class="v-main-wrapper">
    <p>{{ title }}</p>
    <v-catalog />
    <v-card v-if="CART.length" :cart_data="CART" />
  </div>
</template>

<script>
import vCatalog from "./v-catalog.vue";
import vCard from "./v-cart.vue";
import { mapGetters } from "vuex";

export default {
  name: "v-main-wrapper",
  components: {
    vCatalog,
    vCard,
  },
  props: {},
  data() {
    return {
      title: "Main Wrapper",
    };
  },
  computed: {
    ...mapGetters(["CART"]),
  },
  methods: {},
  watch: {},
  mounted() {},
};
</script>

<style>
.v-main-wrapper {
  max-width: 900px;
  margin: 0 auto;
}
</style>
