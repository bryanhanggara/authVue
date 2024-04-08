<template>
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav mx-auto">
        <li class="nav-item">
            <router-link  class="nav-link" to="/">Home</router-link>
        </li>
        <li class="nav-item" v-if="!useAuth.user">
            <router-link  class="nav-link" to="/login">Login</router-link>
        </li>
        <li class="nav-item" v-if="!useAuth.user">
            <router-link  class="nav-link" to="/register">Register</router-link>
        </li>
        <li class="nav-item" v-if="useAuth.user">
            <button class="nav-link"  @click="logout">
              Logout
            </button>
        </li>
      </ul>
    </div>
  </div>
    </nav>
</template>

<script setup>
  import {ref} from 'vue'
    import axios from 'axios'
    import { useRouter } from 'vue-router';
    import { authStore } from '../stores/authstore';

    const router =  useRouter();

    const useAuth = authStore();

    const logout = async () => {
    try {
        await useAuth.getToken();
        await axios.post('/logout');
        router.push('/login');
    } catch (error) {
        console.error("Error logging out:", error);
    }
}

</script>