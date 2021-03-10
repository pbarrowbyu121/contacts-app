<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>First Name:</label>
      <input
        type="text"
        v-model="first_name"
        name="first_name"
        placeholder="First Name"
      />
    </div>
    <div class="form-control">
      <label>Last Name:</label>
      <input
        type="text"
        v-model="last_name"
        name="last_name"
        placeholder="Last Name"
      />
    </div>
    <div class="form-control">
      <label>Phone: </label>
      <input type="text" v-model="phone" name="phone" placeholder="Phone" />
    </div>
    <div class="form-control">
      <label>Email: </label>
      <input
        type="text"
        v-model="email"
        name="email"
        placeholder="email@example.com"
      />
    </div>
    <div class="form-control">
      <label>Address Line 1: </label>
      <input
        type="text"
        v-model="address1"
        name="address1"
        placeholder="Address Line 1"
      />
    </div>
    <div class="form-control">
      <label>Address Line 2: </label>
      <input
        type="text"
        v-model="address2"
        name="address2"
        placeholder="Address Line 2"
      />
    </div>
    <div class="form-control">
      <label>City: </label>
      <input type="text" v-model="city" name="city" placeholder="City" />
    </div>
    <div class="form-control">
      <label>State: </label>
      <input type="text" v-model="state" name="state" placeholder="State" />
    </div>
    <div class="form-control">
      <label>Zip: </label>
      <input type="text" v-model="zip" name="zip" placeholder="Zip" />
    </div>

    <div class="form-control form-control-check">
      <label>Important</label>
      <input type="checkbox" v-model="important" name="important" />
    </div>

    <input type="submit" value="Save Contact" class="btn btn-block" />
  </form>
</template>

<script>
export default {
  name: "NewContact",
  data() {
    return {
      first_name: "",
      last_name: "",
      phone: "",
      address1: "",
      address2: "",
      city: "",
      state: "",
      zip: "",
      email: "",
      important: false,
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();

      if (!this.first_name) {
        alert("Please add first name");
        return;
      }

      const newContact = {
        first_name: this.first_name,
        last_name: this.last_name,
        phone: this.phone,
        address1: this.address1,
        address2: this.address2,
        city: this.city,
        state: this.state,
        zip: this.zip,
        email: this.email,
        important: this.important,
      };

      this.$emit("add-contact", newContact);

      (this.first_name = ""),
        (this.last_name = ""),
        (this.phone = ""),
        (this.address1 = ""),
        (this.address2 = ""),
        (this.city = ""),
        (this.state = ""),
        (this.zip = ""),
        (this.email = ""),
        (this.important = "");
    },
  },
};
</script>

<style scoped>
.form-control {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-left: 6rem;
  margin-right: 6rem;
}

.btn {
  display: flex;
  justify-content: center;
  margin: 1rem auto;
  width: 50%;
  background-color: green;
}
</style>
