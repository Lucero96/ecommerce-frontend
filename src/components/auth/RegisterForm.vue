<template>
  <div class="register-container">
    <form class="register-form" @submit.prevent="registerUser">
      <h3>Crear cuenta</h3>

      <label>Nombre</label>
      <input type="text" v-model="firstName" placeholder="Ingresa tu nombre" required />

      <label>Apellido</label>
      <input type="text" v-model="lastName" placeholder="Ingresa tu apellido" required />

      <label>Email</label>
      <input type="email" v-model="email" placeholder="correo@ejemplo.com" required />

      <label>Contraseña</label>
      <input type="password" v-model="password" placeholder="******" required />

      <label>País</label>
      <input type="text" v-model="country" placeholder="Ej. Perú" />

      <button type="submit">Registrarse</button>

      <p class="login-link">
        ¿Ya tienes cuenta?
        <router-link to="/login">Inicia sesión aquí</router-link>
      </p>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const firstName = ref('')
const lastName = ref('')
const email = ref('')
const password = ref('')
const country = ref('')

const registerUser = async () => {
  try {
    const response = await axios.post('http://localhost:5231/api/User/signup', {
      firstName: firstName.value,
      lastName: lastName.value,
      dateOfBirth: '2000-01-01', // Puedes agregar input si quieres que el usuario lo elija
      country: country.value,
      address: '',
      email: email.value,
      password: password.value,
      type: 'U',
    })

    alert('✅ Registro exitoso. Ahora puedes iniciar sesión.')
    console.log('Usuario creado:', response.data)
  } catch (error) {
    console.error('❌ Error al registrar:', error.response?.data)
    alert(error.response?.data?.message || 'Error al registrar el usuario.')
  }
}
</script>

<style scoped>
.register-container {
  background-color: #080710;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
}

.register-form {
  background: rgba(255, 255, 255, 0.05);
  padding: 40px;
  border-radius: 15px;
  width: 360px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  box-shadow: 0 0 15px rgba(255, 255, 255, 0.1);
}

.register-form h3 {
  text-align: center;
  margin-bottom: 10px;
  color: #ffffff;
}

.register-form label {
  font-size: 14px;
  margin-top: 10px;
}

.register-form input {
  padding: 10px;
  border: none;
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.1);
  color: white;
}

.register-form input::placeholder {
  color: rgba(255, 255, 255, 0.6);
}

.register-form button {
  background-color: #ffffff;
  color: #000;
  padding: 10px;
  margin-top: 20px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
}

.register-form button:hover {
  background-color: #23a2f6;
  color: #fff;
  transition: 0.3s;
}

.login-link {
  text-align: center;
  margin-top: 15px;
  font-size: 14px;
}

.login-link a {
  color: #23a2f6;
  text-decoration: none;
}
</style>
