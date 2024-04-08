<template>
    <div class="container">
        
        <div class="col-md-6 m-auto mt-4">
            <h1>Login Page</h1>
            <form @submit.prevent="submitLogin">
                <div class="mb-3">
                    <label for="exampleInputEmail1" class="form-label">Email address</label>
                    <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" v-model="form.email">
                </div>
                <div class="mb-3">
                    <label for="exampleInputPassword1" class="form-label">Password</label>
                    <input type="password" class="form-control" id="exampleInputPassword1" v-model="form.password">
                </div>
                <button type="submit" class="btn btn-primary">Login</button>
            </form>
        </div>
    </div>
</template>

<script setup>
    import {ref} from 'vue'
    import axios from 'axios'
    import { useRouter } from 'vue-router';
    import { authStore } from '../stores/authstore';

    const router =  useRouter();

    const useAuth = authStore();

    const form = ref({
        email:'',
        password:''
    });

    const submitLogin = async()=>  {
        await useAuth.getToken();
        await axios.post('/login', {
            email: form.value.email,
            password: form.value.password
        });

        router.push('/');
    }
</script>