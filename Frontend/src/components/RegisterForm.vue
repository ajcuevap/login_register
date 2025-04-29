<template>
  <div class="register-page">
    <div class="register-container">
      <div class="register-form">
        <h2 class="title">Regístrate</h2>
        <form @submit.prevent="registerUser">
          <div class="input-group">
            <input v-model="email" type="email" placeholder="Correo electrónico" required />
          </div>
          <div class="input-group">
            <input v-model="password" type="password" placeholder="Contraseña" required />
          </div>
          <div class="input-group">
            <input v-model="confirmPassword" type="password" placeholder="Confirmar Contraseña" required />
          </div>
          <button type="submit" class="submit-btn">Registrar</button>
        </form>
        <p class="login-link">
          ¿Ya tienes cuenta? <router-link to="/login">Inicia sesión aquí</router-link>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'RegisterPage',
  data() {
    return {
      email: '',
      password: '',
      confirmPassword: ''
    };
  },
  methods: {
    async registerUser() {
      if (this.password !== this.confirmPassword) {
        alert('Las contraseñas no coinciden');
        return;
      }
      try {
        await axios.post('http://tu-backend/api/register', {
          email: this.email,
          password: this.password
        });
        alert('Usuario registrado con éxito');
        this.$router.push('/login'); // Redirigir al login después del registro
      } catch (error) {
        alert('Error al registrar usuario');
      }
    }
  }
};
</script>

<style scoped>
.register-page {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(135deg, #ff7e5f, #feb47b); /* Fondo vibrante */
}

.register-container {
  background: rgba(255, 255, 255, 0.9);
  padding: 40px;
  border-radius: 15px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
  width: 400px;
  text-align: center;
  animation: zoomIn 1s ease-out;
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
  border-color: #ff7e5f;
  box-shadow: 0 0 5px rgba(255, 126, 95, 0.5);
}

.submit-btn {
  width: 100%;
  padding: 12px;
  background-color: #ff7e5f;
  border: none;
  color: white;
  font-size: 16px;
  border-radius: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-btn:hover {
  background-color: #feb47b;
}

.login-link {
  margin-top: 20px;
  font-size: 14px;
}

.login-link a {
  color: #ff7e5f;
  text-decoration: none;
  font-weight: 500;
}

.login-link a:hover {
  text-decoration: underline;
}

@keyframes zoomIn {
  0% {
    opacity: 0;
    transform: scale(0.5);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}
</style>
