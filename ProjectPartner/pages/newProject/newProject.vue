<template>
  <view class="container">
    <text class="title">创建新项目</text>
    <view class="form">
      <view class="form-item">
        <text>项目标题</text>
        <input v-model="projectTitle" placeholder="请输入项目标题" />
      </view>
      <view class="form-item">
        <text>项目内容</text>
        <textarea v-model="projectContent" placeholder="请输入项目内容" />
      </view>
      <view class="form-item">
        <text>项目关键词</text>
        <input v-model="projectTags" placeholder="请输入项目关键词，用逗号分隔" />
      </view>
      <button class="submit-button" @click="createProject">创建项目</button>
      <button class="my-created-projects-button" @click="goToMyCreatedProjects">我创建的项目</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      projectTitle: '',
      projectContent: '',
      projectTags: '',
    };
  },
  methods: {
    createProject() {
      if (!this.projectTitle || !this.projectContent) {
        uni.showToast({ title: '请填写所有必填项', icon: 'none' });
        return;
      }

      const newProject = {
        id: Date.now(), // 使用当前时间戳作为项目ID
        name: this.projectTitle,
        description: this.projectContent,
        tags: this.projectTags.split(',').map(tag => tag.trim()), // 将关键词转换为数组
        avatarUrl: 'https://picsum.photos/80/80?random=' + Math.floor(Math.random() * 100), // 随机头像
      };

      // 将新项目保存到本地存储
      let createdProjects = JSON.parse(localStorage.getItem('createdProjects')) || [];
      createdProjects.push(newProject);
      localStorage.setItem('createdProjects', JSON.stringify(createdProjects));

      uni.showToast({ title: '项目创建成功', icon: 'success' });
      this.resetForm(); // 重置表单
    },
    resetForm() {
      this.projectTitle = '';
      this.projectContent = '';
      this.projectTags = '';
    },
    goToMyCreatedProjects() {
      uni.navigateTo({ url: '/pages/myCreatedProjects/myCreatedProjects' });
    },
  },
};
</script>

<style>
.container {
  padding: 20px;
}

.title {
  font-size: 24px;
  text-align: center;
  margin-bottom: 20px;
}

.form {
  margin-bottom: 20px;
}

.form-item {
  margin-bottom: 15px;
}

input, textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

textarea {
  min-height: 100px;
}

.submit-button, .my-created-projects-button {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  border: none;
  border-radius: 5px;
}

.submit-button {
  background-color: #007bff; /* 蓝色 */
  color: white;
}

.my-created-projects-button {
  background-color: #28a745; /* 绿色 */
  color: white;
}
</style>