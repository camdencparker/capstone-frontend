<script>
import axios from "axios";
export default {
  data: function () {
    return {
      user: {},
      // currentUserId: localStorage.user_id
    };
  },
  created: function () {
    axios.get(`/users/1`).then((response) => {
      this.listing = response.data;
      console.log(this.listing);
    });
  },
  methods: {
    destroyListing: function () {
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
    <h2>{{ user.name }}</h2>
    <p>Email: {{ user.email }}</p>
    <p>Phone: {{ user.phone }}</p>
    <p>Location: {{ user.location }}</p>
    <router-link to="/listings">To all listings</router-link>
  </div>
</template>
