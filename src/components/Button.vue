<template>
  <button @click="onClick()" :style="{ background: color }" class="btn">
    {{ text }}
  </button>
</template>

<script>
// import { defineComponent } from '@vue/composition-api'

export default {
  name: "Button",
  props: {
    text: String,
    color: String,
  },
  methods: {
    onClick() {
      //   console.log("click");
      this.$emit("btn-click");
    },
  },
};
</script>
