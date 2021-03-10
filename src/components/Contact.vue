<template>
  <div :class="[contact.important ? 'important' : '', 'contact']">
    <div class="contact-header" @click="showInfo">
      <h3>{{ contact.first_name }} {{ contact.last_name }}</h3>
      <!-- <Button text="Info" color="lightblue" /> -->
    </div>
    <div class="contact-info" v-if="showContactInfo">
      <ContactInfo
        :contact="contact"
        @delete-contact="onDelete"
        @toggle-important="$emit('toggle-important')"
      />
    </div>
  </div>
</template>

<script>
import ContactInfo from "./ContactInfo";
// import Button from "./Button";
export default {
  name: "Contact",
  props: {
    contact: Object,
  },
  components: {
    ContactInfo,
    // Button,
  },
  methods: {
    showInfo() {
      this.showContactInfo = !this.showContactInfo;
    },
    onDelete() {
      this.$emit("delete-contact");
    },
  },
  data() {
    return {
      showContactInfo: false,
    };
  },
};
</script>

<style scoped>
.contact {
  background: #f4f4f4;
  cursor: pointer;
  border: 1px solid gray;
}

.important {
  border-left: 5px solid blue;
}

.contact-header {
  display: flex;
  background: rgb(173, 230, 176);
  align-items: center;
  padding-left: 10px;
  padding-right: 10px;
  border-bottom: 1px solid gray;
}
</style>
