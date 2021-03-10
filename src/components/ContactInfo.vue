<template>
  <div class="contact-phone" v-if="contact.phone">
    <p>Phone:</p>
    <p>{{ contact.phone }}</p>
  </div>
  <div
    class="contact-address"
    v-if="
      contact.address1 ||
        contact.address2 ||
        contact.city ||
        contact.state ||
        contact.zip
    "
  >
    <p>Address:</p>
    <div>
      <p v-if="contact.address1">{{ contact.address1 }}</p>
      <p v-if="contact.address2">{{ contact.address2 }}</p>
      <p v-if="contact.city || contact.state || contact.zip">
        {{ contact.city }}, {{ contact.state }} {{ contact.zip }}
      </p>
    </div>
  </div>
  <div class="contact-email" v-if="contact.email">
    <p>Email:</p>
    <p>{{ contact.email }}</p>
  </div>
  <div class="important-toggle">
    <label>Important:</label>
    <input
      type="checkbox"
      v-model="important"
      @change="$emit('toggle-important')"
      name="important"
    />
  </div>
  <div class="delete-contact">
    <Button text="Delete Contact" color="red" @btn-click="onDelete" />
  </div>
</template>

<script>
import Button from "./Button";
export default {
  name: "ContactInfo",
  props: {
    contact: Object,
  },
  components: {
    Button,
  },
  methods: {
    onDelete() {
      this.$emit("delete-contact");
    },
  },
};
</script>

<style scoped>
.contact-phone,
.contact-address,
.contact-email,
.important-toggle {
  display: flex;
  justify-content: space-between;
  padding-left: 1.5rem;
  padding-right: 1.5rem;
}
</style>
