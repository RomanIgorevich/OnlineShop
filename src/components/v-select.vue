<template>
  <div class="v-select">
    <p class="title" @click="areOptionsVisible = !areOptionsVisible">
      {{ selected }}
    </p>
    <div class="options" v-if="areOptionsVisible">
      <p
        v-for="option of categories"
        :key="option.value"
        @click="selectOption(option)"
      >
      {{ option.name }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "v-select",
  props: {
    categories: {
      type: Array,
      default() {
        return [];
      },
    },
    selected: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      areOptionsVisible: false,
    };
  },
  methods:{
      selectOption(option){
          this.$emit('select', option)
          this.areOptionsVisible = false
      }
  }
};
</script>

<style lang="scss">
.v-select {
  position: relative;
  width: 200px;
  cursor: pointer;
  text-align: left;
}
.title {
  border: solid 1px #aeaeae;
  padding: $padding;
}
.v-select p {
  margin: 0;
}
.options {
  border: solid 1px #aeaeae;
  background: #fff;
  position: absolute;
  top: 30px;
  left: 0;
  width: 100%;
  padding: $padding;
}
.options p:hover {
  background: #e7e7e7;
}
</style>
