<template>
  <div id="app">
    <v-main-wrapper />
  </div>
</template>

<script>
import vMainWrapper from "./components/v-main-wrapper.vue";
import { mapActions, mapGetters } from "vuex";
export default {
  components: {
    vMainWrapper,
  },
  computed: {
    ...mapGetters(["IS_MOBILE", "IS_DESKTOP"]),
  },
  methods: {
    ...mapActions(["SET_MOBILE", "SET_DESKTOP"]),
  },
  mounted() {let vm =this
    window.addEventListener("resize", () => {
      
      if (window.innerWidth > 767) {
        vm.SET_DESKTOP()
        console.log("desctop - "+ vm.IS_DESKTOP);
      } else {
        vm.SET_MOBILE()
        console.log("mobile - "+ vm.IS_MOBILE);
      }
    });
  },
};
</script>
