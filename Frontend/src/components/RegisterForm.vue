<template>
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
        ¿Ya tienes cuenta? <a href="#">Inicia sesión aquí</a>
      </p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'RegisterForm',
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
  } catch (error) {
    alert('Error al registrar usuario');
  }
}
  }
};
</script>

<style scoped>
.register-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(to left, #ff7e5f, #feb47b); 
}

.register-form {
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
  border-radius: 5px;
  cursor: pointer;
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
}

.login-link a:hover {
  text-decoration: underline;
}
</style>
