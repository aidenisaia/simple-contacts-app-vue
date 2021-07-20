<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <p>First name: <input type="text" v-model="contactNewParams.first_name"/></p>
    <p>Last name: <input type="text" v-model="contactNewParams.last_name"/></p>
    <p>Email: <input type="text" v-model="contactNewParams.email"/></p>
    <p>Phone number: <input type="text" v-model="contactNewParams.phone_number"/></p>
    <p>Image: <input type="text" v-model="contactNewParams.image"/></p>
    <button v-on:click="contactCreate()">New Contact</button>
    <h2 v-for="contact in contacts">
      <p> {{contact.first_name}}, {{contact.last_name}}  </p>
      <p> {{contact.phone_number}} </p>
      <p> {{contact.email}} </p>
      p> {{contact.image}} </p>
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
      contactNewParams: {},
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
      var contactParams = {
        first_name: this.contactNewParams.first_name,
        last_name: this.contactNewParams.last_name,
        email: this.contactNewParams.email,
        phone_number: this.contactNewParams.phone_number,
        image: this.contactNewParams.image,
      };
      console.log(contactParams);
      axios.post("contacts", contactParams).then((response) => {
        console.log(response.data);
        this.contacts.push(response.data);
      });
    },
  },
};
</script>
