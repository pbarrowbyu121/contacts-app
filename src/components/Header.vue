<template>
  <header>
    <h1>
      {{ title }}
    </h1>
    <Button
      text="New Contact"
      color="blue"
      @btn-click="$emit('toggle-new-contact')"
    />
  </header>
</template>

<script>
import Button from "./Button";
export default {
  name: "Header",
  props: ["title"],
  components: {
    Button,
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
