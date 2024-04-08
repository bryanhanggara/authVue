<template>
    <div class="container">
        
        <div class="col-md-6 m-auto mt-4">
            <h1>Register Page</h1>
            <form @submit.prevent="submitRegister">
                <div class="mb-3">
                    <label for="exampleInputName" class="form-label">Name</label>
                    <input type="text" class="form-control" id="exampleInputName" v-model="form.name">
                </div>
                <div class="mb-3">
                    <label for="exampleInputEmail1" class="form-label">Email address</label>
                    <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" v-model="form.email">
                </div>
                <div class="mb-3">
                    <label for="exampleInputPassword1" class="form-label">Password</label>
                    <input type="password" class="form-control" id="exampleInputPassword1" v-model="form.password">
                </div>
                <div class="mb-3">
                    <label for="exampleInputConfirmPassword" class="form-label">Confirm Password</label>
                    <input type="password" class="form-control" id="exampleInputConfirmPassword" v-model="form.password_confirmation">
                </div>
                <button type="submit" class="btn btn-primary">Register</button>
            </form>
        </div>
    </div>
</template>

<script setup>
    import { ref } from 'vue'
    import axios from 'axios'
    import { useRouter } from 'vue-router';
    import { authStore } from '../stores/authstore';

    const useAuth = authStore();

    const router = useRouter();

    const form = ref({
        name: '',
        email:'',
        password:'',
        password_confirmation: ''
    });

    const submitRegister = async () =>  {
        await useAuth.getToken();
        if (form.value.password !== form.value.password_confirmation) {
            alert("Password and confirm password do not match");
            return;
        }
        
        try {
            // Melakukan permintaan pendaftaran
            const response = await axios.post('/register', {
                name: form.value.name,
                email: form.value.email,
                password: form.value.password,
                password_confirmation: form.value.password_confirmation
            });

            // Jika pendaftaran berhasil, redirect ke halaman utama
            router.push('/');
        } catch (error) {
            // Jika terjadi kesalahan, tampilkan pesan kesalahan atau lakukan penanganan kesalahan yang sesuai
            console.error("Error registering:", error);
        }
    }
</script>
