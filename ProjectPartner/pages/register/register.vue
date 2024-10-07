<template>
  <div class="register">
    <h1>注册账号</h1>
    <form @submit.prevent="register">
      <div>
        <label for="username">用户名</label>
        <input type="text" v-model="username" placeholder="请输入用户名" required />
      </div>
      <div>
        <label for="password">密码</label>
        <input type="password" v-model="password" placeholder="请输入密码" required />
      </div>
      <div>
        <label for="confirmPassword">确认密码</label>
        <input type="password" v-model="confirmPassword" placeholder="确认密码" required />
      </div>
      <div>
        <label for="email">邮箱</label>
        <input type="email" v-model="email" placeholder="请输入邮箱" required />
      </div>
      <div>
        <label for="phone">手机号码</label>
        <input type="tel" v-model="phone" placeholder="请输入手机号码" required />
      </div>
      <button type="submit">确认注册</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
      confirmPassword: '',
      email: '',
      phone: ''
    };
  },
  methods: {
    async register() {
      // 简单的表单验证
      if (this.password !== this.confirmPassword) {
        alert('密码不匹配');
        return;
      }

      // 发送注册请求（假设有一个 API）
      try {
        const response = await this.$http.post('/api/register', {
          username: this.username,
          password: this.password,
          email: this.email,
          phone: this.phone
        });

        if (response.data.success) {
          // 注册成功，返回登录页面
          this.$router.push({ path: 'D:/Users/Documents/HBuilderProjects/ProjectPartner/pages/Login/Login.vue' });
        } else {
          alert(response.data.message);
        }
      } catch (error) {
        console.error(error);
        alert('注册失败，请重试');
      }
    }
  }
};
</script>

<style scoped>
.register {
  max-width: 400px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
h1 {
  text-align: center;
}
form div {
  margin-bottom: 15px;
}
</style>
