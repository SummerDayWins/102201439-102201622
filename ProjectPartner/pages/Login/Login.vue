<template>
	<view class="container">
		<text class="title">跨学汇</text>
		<input class="input" placeholder="请输入用户名" v-model="username" />
		<input class="input" placeholder="请输入密码" v-model="password" type="password" />
		<button class="button" @click="login">登录</button>
		<button class="button" @click="register">注册</button>
		<text class="other-login">-- 或用其他账号登录 --</text>
	</view>
</template>

<script>
export default {
	data() {
		return {
			username: '',
			password: '',
			registeredUsers: [] // 新增：用于存储注册的用户
		}
	},
	methods: {
		login() {
			// 登录逻辑
			if (!this.username || !this.password) { // 新增：检查用户名和密码是否为空
				uni.showToast({
					title: '用户名和密码不能为空',
					icon: 'none', // 显示为无图标
					duration: 2000 // 持续时间
				});
				return; // 如果为空，直接返回
			}
			if (!this.registeredUsers.includes(this.username)) {
				uni.showToast({
					title: '账号不存在',
					icon: 'none',
					duration: 2000
				});
				return; // 如果账号不存在，直接返回
			}
			// 这里可以添加密码验证逻辑
			console.log('用户名:', this.username);
			console.log('密码:', this.password);
			// 这里可以添加 API 调用
			uni.navigateTo({
				url: '/pages/square/square' 
			});
		},
		register() {
			// 注册逻辑
			if (!this.registeredUsers.includes(this.username)) {
				this.registeredUsers.push(this.username); // 新增：将注册的用户添加到数组中
				uni.showToast({
					title: '注册成功',
					icon: 'success',
					duration: 2000
				});
			} else {
				uni.showToast({
					title: '账号已存在',
					icon: 'none',
					duration: 2000
				});
			}
			uni.navigateTo({
				url: '/pages/register/register' 
			});
		},

	}
}
</script>

<style>
.container {
	padding: 20px;
	text-align: center;
}
.title {
	font-size: 50px;
	margin-bottom: 20px;
}
.input {
	width: 100%;
	padding: 10px;
	margin-bottom: 15px;
	border: 1px solid #ccc;
	border-radius: 5px;
}
.button {
	width: 100%;
	padding: 10px;
	background-color: #007AFF;
	color: white;
	border: none;
	border-radius: 5px;
	margin-bottom: 10px;
}
.other-login {
	margin: 10px 0;
}
.social-login {
	display: flex;
	justify-content: center;
}
.icon {
	width: 40px;
	height: 40px;
	margin: 0 10px;
}
</style>