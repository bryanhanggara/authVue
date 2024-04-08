<template>
    <h2>Home Page</h2>
    <div v-if="useAuth.user">
        <h5>{{ useAuth.user.name }}</h5>
        <h6>{{ useAuth.user.email }}</h6>
    </div>
    <div v-if="!useAuth.user">
        No Data
    </div>
    

</template>

<script setup>
    import { ref,onMounted } from 'vue';
    import axios from 'axios'

    import { authStore } from '../stores/authstore';

    const useAuth = authStore();

    const user = ref();

    onMounted(async () => {
        useAuth.getUser();
    })
</script>