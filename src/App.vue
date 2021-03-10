<template>
  <div class="container">
    <Header title="Contacts App" @toggle-new-contact="toggleNewContact" />
    <NewContact v-if="showNewContact" @add-contact="addContact" />
    <Contacts
      :contacts="contacts"
      @delete-contact="deleteContact"
      @toggle-important="toggleImportant"
    />
  </div>
</template>

<script>
import Header from "./components/Header";
import Contacts from "./components/Contacts";
import NewContact from "./components/NewContact";

export default {
  name: "App",
  components: {
    Header,
    Contacts,
    NewContact,
  },
  data() {
    return {
      contacts: [],
      showNewContact: false,
    };
  },

  methods: {
    async addContact(contact) {
      const res = await fetch("api/contacts", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(contact),
      });
      const data = await res.json();
      this.contacts = [...this.contacts, data];
    },
    async deleteContact(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/contacts/${id}`, {
          method: "DELETE",
        });
        res.status === 200
          ? (this.contacts = this.contacts.filter(
              (contact) => contact.id !== id
            ))
          : alert("Error deleting task");
      }
    },
    async toggleImportant(id) {
      const contactToToggle = await this.fetchContact(id);
      const updContact = {
        ...contactToToggle,
        important: !contactToToggle.important,
      };
      const res = await fetch(`api/contacts/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updContact),
      });
      const data = await res.json();
      this.contacts = this.contacts.map((contact) =>
        contact.id === id ? { ...contact, important: data.important } : contact
      );
    },
    toggleNewContact() {
      this.showNewContact = !this.showNewContact;
      console.log("show New Contact");
    },
    async fetchContacts() {
      const res = await fetch(`api/contacts`);
      const data = await res.json();
      console.log("data", data);
      return data;
    },
    async fetchContact(id) {
      const res = await fetch(`api/contacts/${id}`);
      const data = await res.json();

      return data;
    },
    compareValues(key, order = "asc") {
      return function innerSort(a, b) {
        if (
          !a.prototype.hasOwnProperty.call(key) ||
          !b.prototype.hasOwnProperty.call(key)
        ) {
          // property doesn't exist on either object
          return 0;
        }

        const varA = typeof a[key] === "string" ? a[key].toUpperCase() : a[key];
        const varB = typeof b[key] === "string" ? b[key].toUpperCase() : b[key];

        let comparison = 0;
        if (varA > varB) {
          comparison = 1;
        } else if (varA < varB) {
          comparison = -1;
        }
        return order === "desc" ? comparison * -1 : comparison;
      };
    },
  },
  async created() {
    let fetchedData = await this.fetchContacts();
    fetchedData.sort((a, b) => (a.last_name > b.last_name ? 1 : -1));
    this.contacts = fetchedData;
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 75%;
}
</style>
