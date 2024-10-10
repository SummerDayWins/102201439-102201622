<template>
  <div class="container">
    <h1>广场大厅</h1>
    <div class="circle-container">
      <div class="circle" @click="profile()">
        <span>个人简历</span>
      </div>
      <div class="circle" @click="addProject()">
        <span>加入项目</span>
      </div>
      <div class="circle" @click="newProject()">
        <span>新建项目</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    navigateTo(page) {
      // 根据页面名称进行导航
      this.$router.push({ name: page });
    },
	profile() {
		uni.navigateTo({
			url: '/pages/profile/profile' 
		});
	},
	addProject() {
		uni.navigateTo({
			url: '/pages/addProject/addProject' 
		});
	},
	newProject() {
		uni.navigateTo({
			url: '/pages/newProject/newProject' 
		});
	},
  }
};
</script>

<style scoped>
.container {
  text-align: center;
  padding: 20px;
}

.circle-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 50px;
}

.circle {
  width: 120px;
  height: 120px;
  border-radius: 60px;
  border: 2px solid #007bff;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 20px;
  position: relative;
  cursor: pointer;
  transition: transform 0.2s;
}

.circle:hover {
  transform: scale(1.05);
}

.badge {
  background-color: red;
  color: white;
  border-radius: 50%;
  padding: 5px 10px;
  position: absolute;
  top: 10px;
  right: 10px;
}
</style>