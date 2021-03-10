<template>
  <div :key="contact.id" v-for="contact in contacts">
    <Contact
      :contact="contact"
      @delete-contact="onDelete(contact.id)"
      @toggle-important="$emit('toggle-important', contact.id)"
    />
  </div>
</template>

<script>
import Contact from "./Contact";

export default {
  name: "Contacts",
  props: {
    contacts: Array,
  },
  components: {
    Contact,
  },
  methods: {
    onDelete(id) {
      console.log("delete id Contacts", id);
      this.$emit("delete-contact", id);
    },
  },
};
</script>
