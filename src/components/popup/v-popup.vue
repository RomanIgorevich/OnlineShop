<template>
  <div class="popup_wrapper" ref="popup_wrapper">
    <div class="v-popup">
      <div class="v-popup__header">
        <span>{{ popupTitle }}</span>
        <span>
          <i @click="closePopup" class="material-icons">close</i>
        </span>
      </div>
      <div class="v-popup__content">
        <slot></slot>
      </div>
      <div class="v-popup__footer">
        <button class="close_modal" @click="closePopup">Close</button>
        <button class="submit_btn" @click="rightBtnAction">{{ rightBtnTitle }}</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-popup",
  components: {},
  props: {
    popupTitle: {
      type: String,
      default: "Popup name",
    },

    rightBtnTitle: {
      type: String,
      default: "Ок",
    },
  }, 
  data() {
    return {};
  },
  computed: {},
  methods: {
    closePopup() {
      this.$emit("closePopup");
    },
    rightBtnAction(){
        this.$emit("rightBtnAction")
    }
  },
  watch: {},
  mounted() {
    let vm = this;
    document.addEventListener("click", (item) => {
      if (item.target === vm.$refs["popup_wrapper"]) {
        vm.closePopup();
      }
    });
  },
};
</script>

<style lang="scss">
.popup_wrapper {
  background: rgba($color: #747474, $alpha: 0.4);
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  right: 0;
  left: 0;
  top: 0;
  bottom: 0;
}
.v-popup {
  padding: $padding * 2;
  position: fixed;
  top: 50px;
  width: 400px;
  background: #fff;
  box-shadow: 0 0 17px 0 #e7e7e7;
  z-index: 3;
  &__header,
  &__footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  &__content {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .submit_btn {
    padding: $padding;
    color: #fff;
    background: #26ae68;
  }
  .close_modal {
    padding: $padding;
    color: #fff;
    background: rgb(224, 60, 31);
  }
}
</style>
