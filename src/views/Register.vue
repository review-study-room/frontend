<template>
    <div class="register-container">
      <h1>Register</h1>
      <form @submit.prevent="handleRegister">
        <!-- 用户名输入框 -->
        <div class="form-group">
          <label for="username">Username:</label>
          <input v-model="registerForm.username" type="text" id="username" placeholder="Enter username" required>
        </div>
        <!-- 密码输入框 -->
        <div class="form-group">
          <label for="password">Password:</label>
          <input v-model="registerForm.password" type="password" id="password" placeholder="Enter password" required>
        </div>
        <!-- 确认密码输入框 -->
        <div class="form-group">
          <label for="confirmPassword">Confirm Password:</label>
          <input v-model="registerForm.confirmPassword" type="password" id="confirmPassword" placeholder="Confirm password" required>
        </div>
        <!-- 注册按钮 -->
        <button type="submit" class="btn btn-primary">Register</button>
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import { ref } from 'vue';
  import { useRouter } from 'vue-router';
  
  export default {
    setup() {
      const router = useRouter();
      const registerForm = ref({
        username: '',
        password: '',
        confirmPassword: ''
      });
  
      // 处理注册
      const handleRegister = async () => {
        if (registerForm.value.password !== registerForm.value.confirmPassword) {
          alert("Passwords do not match.");
          return;
        }
  
        try {
          const response = await axios.post('http://yourapi.com/register', {
            username: registerForm.value.username,
            password: registerForm.value.password
          });
          alert("Registration successful!");
          router.push('/login.html');
        } catch (error) {
          alert('Registration failed: ' + error.response.data.message);
        }
      };
  
      return {
        registerForm,
        handleRegister
      };
    }
  }
  </script>
  
  <style scoped>
  /* 样式定义 */
  .register-container {
    max-width: 300px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    text-align: center;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  input[type="text"],
  input[type="password"] {
    width: 100%;
    padding: 8px;
    box-sizing: border-box;
  }
  
  .btn {
    width: 100%;
    padding: 8px;
    margin-top: 10px;
  }
  
  .btn-primary {
    background-color: #007bff;
    color: white;
    border: none;
  }
  </style>
  