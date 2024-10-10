<template>
  <view class="container">
    <text class="title">我创建的项目</text>
    <view class="project-list">
      <view class="project-card" v-for="project in createdProjects" :key="project.id">
        <view class="project-header">
          <view class="avatar" :style="{ backgroundImage: 'url(' + project.avatarUrl + ')' }"></view>
          <view class="project-info">
            <text class="project-name">{{ project.name }}</text>
            <text class="project-description">介绍：{{ project.description }}</text>
            <view class="tags">
              <text class="tag" v-for="tag in project.tags" :key="tag">{{ tag }}</text>
            </view>
          </view>
        </view>
        <button class="remove-button" @click="removeProject(project.id)">移除</button>
      </view>
      <text v-if="createdProjects.length === 0" class="no-projects">您还没有创建任何项目。</text>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      createdProjects: [],
    };
  },
  onShow() {
    this.loadCreatedProjects();
  },
  methods: {
    loadCreatedProjects() {
      const projects = JSON.parse(localStorage.getItem('createdProjects')) || [];
      this.createdProjects = projects;
    },
    removeProject(projectId) {
      this.createdProjects = this.createdProjects.filter(project => project.id !== projectId);
      localStorage.setItem('createdProjects', JSON.stringify(this.createdProjects));
      uni.showToast({ title: '项目已移除', icon: 'success' });
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

.project-list {
  margin-bottom: 20px;
}

.project-card {
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 10px;
  margin-bottom: 10px;
}

.project-header {
  display: flex;
  align-items: center;
}

.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background-color: #ccc;
  margin-right: 10px;
  background-size: cover;
}

.project-info {
  flex: 1;
}

.project-name {
  font-size: 18px;
  font-weight: bold;
}

.project-description {
  color: #666;
}

.tags {
  margin-top: 5px;
}

.tag {
  display: inline-block;
  background-color: #007bff;
  color: white;
  padding: 5px;
  border-radius: 5px;
  margin-right: 5px;
}

.no-projects {
  text-align: center;
  color: #999;
}

.remove-button {
  margin-top: 10px;
  padding: 10px;
  background-color: #dc3545; /* 红色 */
  color: white;
  border: none;
  border-radius: 5px;
  width: 100%; /* 确保按钮宽度 */
}
</style>