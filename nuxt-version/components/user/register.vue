<script setup>
import { ref } from 'vue';

const formData = ref({ email: '', password: '' });
const error = ref(false);
const success = ref(false);
const errorMessage = ref('');

async function handleSubmit(e) {
  try {
    e.preventDefault();
    await $fetch('/api/register', {
      method: 'POST',
      body: formData.value,
    });
    success.value = true;
  } catch (err) {
    console.error('Error:', err);
    error.value = true;
    errorMessage.value = err.message;
  }
}
</script>

<template>
  <div class="container mt5">
    <h1>Register</h1>
    <form class="mt-3" action="#" @submit="handleSubmit">
      <div class="mb-3">
        <label for="email" class="form-label">Email address</label>
        <input
          id="email"
          v-model="formData.email"
          type="email"
          class="form-control"
          required
        />
      </div>
      <div class="mb-3">
        <label html="password" class="form-label">Password</label>
        <input
          id="password"
          v-model="formData.password"
          type="password"
          class="form-control"
          required
        />
      </div>
      <div v-if="error" class="alert alert-danger">{{ errorMessage }}</div>
      <div v-if="success" class="alert alert-success">
        You are now register, please login now!
      </div>
      <button type="submit" class="btn btn-primary">Register</button>
    </form>
  </div>
</template>

<style lang="scss">
@import '../../node_modules/bootstrap/scss/functions';
@import '../../node_modules/bootstrap/scss/mixins';
@import '../../node_modules/bootstrap/scss/variables';
@import '../../node_modules/bootstrap/scss/forms';
@import '../../node_modules/bootstrap/scss/buttons';
@import '../../node_modules/bootstrap/scss/alert';
</style>
