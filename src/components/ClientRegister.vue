<template>
  <div class="registration-container">
    <h2>New Client Registration</h2>
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label for="name">Name *</label>
        <input type="text" id="name" v-model="form.name" required />
      </div>

      <div class="form-group">
        <label for="dob">DOB *</label>
        <input type="date" id="dob" v-model="form.dob" required />
      </div>

      <div class="form-group">
        <label for="gender">Gender *</label>
        <select id="gender" v-model="form.gender" required>
          <option value="">Select</option>
          <option value="male">Male</option>
          <option value="female">Female</option>
        </select>
      </div>

      <div class="form-group">
        <label for="phone">Phone Number *</label>
        <input type="tel" id="phone" v-model="form.phone" required />
      </div>

      <div class="form-group">
        <label for="address">Address *</label>
        <textarea id="address" v-model="form.address" required></textarea>
      </div>

      <button type="submit">Register</button>
    </form>
  </div>
</template>

<script>
import { API, graphqlOperation } from "aws-amplify";
import { createClient } from "@/graphql/mutations"; // Import your GraphQL mutation

export default {
  data() {
    return {
      form: {
        name: "",
        dob: "",
        gender: "",
        phone: "",
        address: "",
      },
    };
  },
  methods: {
    async submitForm() {
      try {
        const newClient = await API.graphql(
          graphqlOperation(createClient, { input: this.form })
        );
        console.log("Client Registered:", newClient);
        alert("Registration Successful!");
      } catch (error) {
        console.error("Error registering client:", error);
      }
    },
  },
};
</script>

<style>
.registration-container {
  width: 50%;
  margin: auto;
  padding: 20px;
  background: #fff;
  border-radius: 5px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

.form-group {
  margin-bottom: 15px;
}

input, select, textarea {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  background: #007bff;
  color: white;
  border: none;
  padding: 10px 15px;
  cursor: pointer;
}
</style>
