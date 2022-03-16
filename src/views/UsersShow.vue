<script>
import axios from "axios";
export default {
  data: function () {
    return {
      user: {},
      listing: {},
      // currentUserId: localStorage.user_id
    };
  },
  created: function () {
    axios.get(`/users/1`).then((response) => {
      this.user = response.data;
      console.log(this.user);
    });
  },
  methods: {
    destroyUser: function () {
      if (confirm("Are you sure you to delete this?")) {
        axios.delete(`/users/${this.user.id}`).then((response) => {
          console.log("Success", response.data);
          this.$router.push("/users");
        });
      }
    },
  },
};
</script>

<template>
  <div class="users-show">
    <h2>{{ this.user.name }}</h2>
    <img v-bind:src="this.user.profile_pic" v-bind:alt="this.user.id" />
    <p>Email: {{ this.user.email }}</p>
    <p>Phone: {{ this.user.phone }}</p>
    <p>Location: {{ this.user.location }}</p>
    <div v-for="listing in this.user.listings" v-bind:key="listing.id">
      <p>{{ listing.brand }}</p>
      <router-link v-bind:to="`/listings/${listing.id}`">
        <img v-bind:src="this.listing.image_url" v-bind:alt="listing.id" />
      </router-link>
    </div>
    <button v-on:click="destroyUser()">Delete Profile</button>
    <br />
    <router-link to="/listings">To all listings</router-link>
  </div>
</template>
