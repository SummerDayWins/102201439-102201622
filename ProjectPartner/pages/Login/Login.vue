<template>
	<view class="container">
		<text class="title">跨学汇</text>
		<input class="input" placeholder="请输入用户名" v-model="username" />
		<input class="input" placeholder="请输入密码" v-model="password" type="password" />
		<button class="button" @click="login">登录</button>
		<button class="button" @click="register">注册</button>
		<text class="other-login">-- 或用其他账号登录 --</text>
		<view class="social-login">
			<image src="path/to/wechat-icon.png" class="icon" @click="loginWithWeChat" />
			<image src="path/to/qq-icon.png" class="icon" @click="loginWithQQ" />
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			username: '',
			password: ''
		}
	},
	methods: {
		login() {
			// 登录逻辑
			console.log('用户名:', this.username);
			console.log('密码:', this.password);
			// 这里可以添加 API 调用
		},
		register() {
			// 注册逻辑
			console.log('跳转到注册页面');
			uni.navigateTo({
				url: '/pages/register/register' // 替换为注册页面的路径
			});
		},
		loginWithWeChat() {
			// 微信登录逻辑
			console.log('使用微信登录');
		},
		loginWithQQ() {
			// QQ 登录逻辑
			console.log('使用QQ登录');
		}
	}
}
</script>

<style>
.container {
	padding: 20px;
	text-align: center;
}
.title {
	font-size: 24px;
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