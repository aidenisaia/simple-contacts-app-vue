<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <hr>
    <h2 v-for="contact in contacts">
      <p> {{contact.first_name}}, {{contact.last_name}}  </p>
      <p> {{contact.phone_number}} </p> 
      <hr> 
    </h2>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      contacts: [],
      contactNew: {},
    };
  },
  created: function () {
    axios.get("contacts").then((response) => {
      this.contacts = response.data;
      console.log(this.contacts);
    });
  },
  methods: {
    contactCreate: function () {
      axios.post("contacts").then(response) => {
        response = this.contactNew
      }
    }
  },
};
</script>
