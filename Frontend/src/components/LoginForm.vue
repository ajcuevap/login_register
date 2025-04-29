<template>
  <div class="login-page">
    <div class="login-container">
      <div class="login-form">
        <h2 class="title">Iniciar sesión</h2>
        <form @submit.prevent="loginUser">
          <div class="input-group">
            <input v-model="email" type="email" placeholder="Correo electrónico" required />
          </div>
          <div class="input-group">
            <input v-model="password" type="password" placeholder="Contraseña" required />
          </div>
          <button type="submit" class="submit-btn">Iniciar sesión</button>
        </form>
        <p class="signup-link">
          ¿No tienes una cuenta? <router-link to="/register">Regístrate aquí</router-link>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'LoginPage',
  data() {
    return {
      email: '',
      password: ''
    };
  },
  methods: {
    async loginUser() {
      try {
        const response = await axios.post('http://tu-backend/api/login', {
          email: this.email,
          password: this.password
        });
        localStorage.setItem('token', response.data.token);
        this.$router.push('/dashboard'); // Redirigir al dashboard después de login
        alert('Inicio de sesión exitoso');
      } catch (error) {
        alert('Credenciales incorrectas');
      }
    }
  }
};
</script>

<style scoped>
.login-page {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: radial-gradient(circle, #a1c4fd, #c2e9fb); /* Fondo atractivo */
}

.login-container {
  background: rgba(255, 255, 255, 0.85);
  padding: 40px;
  border-radius: 15px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
  width: 400px;
  text-align: center;
  animation: bounceIn 1s ease-out;
}

.title {
  font-size: 30px;
  font-weight: bold;
  color: #333;
  margin-bottom: 25px;
  text-transform: uppercase;
}

.input-group {
  margin-bottom: 20px;
}

input {
  width: 100%;
  padding: 12px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 10px;
  outline: none;
  transition: all 0.3s ease;
}

input:focus {
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.submit-btn {
  width: 100%;
  padding: 12px;
  background-color: #007bff;
  border: none;
  color: white;
  font-size: 16px;
  border-radius: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-btn:hover {
  background-color: #0056b3;
}

.signup-link {
  margin-top: 20px;
  font-size: 14px;
}

.signup-link a {
  color: #007bff;
  text-decoration: none;
  font-weight: 500;
}

.signup-link a:hover {
  text-decoration: underline;
}

@keyframes bounceIn {
  0% {
    opacity: 0;
    transform: translateY(-50px);
  }
  60% {
    opacity: 1;
    transform: translateY(10px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
