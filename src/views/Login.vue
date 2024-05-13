<template>
    <div class="login-container">
      <h1>Login</h1>
      <form @submit.prevent="handleLogin">
        <!-- 用户名输入框 -->
        <div class="form-group">
          <label for="username">Username:</label>
          <input v-model="loginForm.username" type="text" id="username" placeholder="Enter username" required>
        </div>
        <!-- 密码输入框 -->
        <div class="form-group">
          <label for="password">Password:</label>
          <input v-model="loginForm.password" type="password" id="password" placeholder="Enter password" required>
        </div>
        <!-- 登录按钮 -->
        <button type="submit" class="btn btn-primary">Login</button>
      </form>
      <!-- 注册按钮 -->
      <button @click="goToRegister" class="btn btn-secondary">Register</button>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import { ref } from 'vue';
  import { useRouter } from 'vue-router';
  
  export default {
    setup() {
      const router = useRouter();
      const loginForm = ref({
        username: '',
        password: ''
      });
  
      // 处理登录
      const handleLogin = async () => {
        try {
          const response = await axios.post('http://yourapi.com/login', loginForm.value);
          // 根据权限跳转
          if (response.data.permission === 0) {
            router.push('/manage.html');
          } else if (response.data.permission === 1) {
            router.push('/reserve.html');
          }
        } catch (error) {
          alert('Login failed: ' + error.message);
        }
      };
  
      // 跳转到注册页面
      const goToRegister = () => {
        router.push('/register.html');
      };
  
      return {
        loginForm,
        handleLogin,
        goToRegister
      };
    }
  }
  </script>
  
  <style scoped>
  /* 样式定义 */
  .login-container {
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
  
  .btn-secondary {
    background-color: #6c757d;
    color: white;
    border: none;
  }
  </style>
  