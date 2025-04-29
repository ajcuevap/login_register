<template>
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
        ¿No tienes una cuenta? <a href="#">Regístrate aquí</a>
      </p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'LoginForm',
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
        alert('Inicio de sesión exitoso');
      } catch (error) {
        alert('Credenciales incorrectas');
      }
    }
  }
};
</script>

<style scoped>
/* Estilo general para el contenedor de login */
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(to right, #00b4db, #0083b0); /* Fondo degradado */
}

.login-form {
  background: #fff;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 350px;
  text-align: center;
}

.title {
  font-size: 24px;
  font-weight: 600;
  color: #333;
  margin-bottom: 20px;
}

.input-group {
  margin-bottom: 20px;
}

input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 5px;
  outline: none;
}

input:focus {
  border-color: #00b4db;
  box-shadow: 0 0 5px rgba(0, 180, 219, 0.5);
}

.submit-btn {
  width: 100%;
  padding: 12px;
  background-color: #00b4db;
  border: none;
  color: white;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
}

.submit-btn:hover {
  background-color: #0083b0;
}

.signup-link {
  margin-top: 20px;
  font-size: 14px;
}

.signup-link a {
  color: #00b4db;
  text-decoration: none;
}

.signup-link a:hover {
  text-decoration: underline;
}
</style>
