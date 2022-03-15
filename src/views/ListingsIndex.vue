<script>
import axios from "axios";
export default {
  data: function () {
    return {
      listings: [],
    };
  },
  created: function () {
    this.indexListings();
  },
  methods: {
    indexListings: function () {
      axios.get("/listings").then((response) => {
        console.log("listings index", response);
        this.listings = response.data;
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>All Listings</h1>
    <div v-for="listing in listings" v-bind:key="listing.id">
      <h2>{{ listing.name }}</h2>
      <!-- <img v-bind:src="listing.image_url" v-bind:alt="listing.name" /> -->
      <p>Brand: {{ listing.brand }}</p>
      <p>model: {{ listing.model }}</p>
      <router-link v-bind:to="`/listings/${listing.id}`">{{ listing.name }}</router-link>
    </div>
  </div>
</template>
