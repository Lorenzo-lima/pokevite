<script setup>
import { ref } from "vue"
</script>

<template>
  <!-- Navbar -->
  <nav class="navbar navbar-dark navbar-expand-lg  bg-primary bg-gradient text-primary-light">
    <div class="container-fluid d-flex align-items-center">
      <router-link class="navbar-brand" to="/">
        <img 
        src="./assets/pikechu.svg" alt="Logo" width="30" class="d-inline-block justify-center">
        Pokevite
      </router-link>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <router-link class="nav-link" aria-current="page" to="/">Home</router-link>
          <router-link class="nav-link" to="/about">About</router-link>
        </div>
      </div>
    </div>
  </nav>

  <!-- Content -->
  <div class="main">
    <router-view></router-view>
  </div>
</template>

<style scoped>
  
</style>
