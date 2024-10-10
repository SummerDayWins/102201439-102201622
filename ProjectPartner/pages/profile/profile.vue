<template>
  <div class="profile">
    <div class="header">
      <div 
        class="avatar" 
        :style="{ backgroundImage: 'url(' + avatarUrl + ')' }"
      >
        头像
      </div>
      <div class="user-info">
        <h2>{{ username }}</h2>
        <p>个性签名：<span v-if="!isEditing">{{ signature }}</span><input v-if="isEditing" v-model="signature" /></p>
        <p>电话：<span v-if="!isEditing">{{ phone }}</span><input v-if="isEditing" v-model="phone" /></p>
        <p>邮箱：<span v-if="!isEditing">{{ email }}</span><input v-if="isEditing" v-model="email" /></p>
        <p>QQ：<span v-if="!isEditing">{{ qq }}</span><input v-if="isEditing" v-model="qq" /></p>
      </div>
    </div>
    <div class="tabs">
      <button @click="showEducation = false" class="active">项目经历</button>
    </div>
    <div class="content">
      <div v-if="!showEducation">
        <h3>项目经历</h3>
        <div v-if="joinedProjects.length === 0 && createdProjects.length === 0">没有项目经历</div>
        <div v-else>
          <div class="project-list">
            <div class="project-card" v-for="project in joinedProjects" :key="project.id">
              <div class="project-header">
                <div class="avatar" :style="{ backgroundImage: 'url(' + project.avatarUrl + ')' }"></div>
                <div class="project-info">
                  <h4 class="project-name">{{ project.name }}</h4>
                  <p class="project-description">介绍：{{ project.description }}</p>
                  <div class="tags">
                    <span class="tag" v-for="tag in project.tags" :key="tag">{{ tag }}</span>
                  </div>
                </div>
              </div>
            </div>
            <div class="project-card" v-for="project in createdProjects" :key="project.id">
              <div class="project-header">
                <div class="avatar" :style="{ backgroundImage: 'url(' + project.avatarUrl + ')' }"></div>
                <div class="project-info">
                  <h4 class="project-name">{{ project.name }}</h4>
                  <p class="project-description">介绍：{{ project.description }}</p>
                  <div class="tags">
                    <span class="tag" v-for="tag in project.tags" :key="tag">{{ tag }}</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <button class="edit-button" @click="toggleEdit">
      {{ isEditing ? '保存' : '编辑' }}
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isEditing: false, // 编辑状态
      username: '用户名',
      signature: '个性签名',
      phone: '1234567890',
      email: 'example@example.com',
      qq: '123456789',
      showEducation: false, // 默认不显示教育经历
      avatarUrl: '', // 直接使用随机头像 URL
      joinedProjects: [], // 新增属性以存储项目经历
      createdProjects: [], // 新增属性以存储创建的项目
    };
  },
  created() {
    this.loadData(); // 组件创建时加载数据
    this.loadJoinedProjects(); // 加载项目经历
    this.loadCreatedProjects(); // 加载创建的项目
    this.generateRandomAvatar(); // 生成随机头像
  },
  methods: {
    generateRandomAvatar() {
      // 生成随机头像 URL
      this.avatarUrl = `https://api.adorable.io/avatars/80/${Math.random()}.png`;
    },
    toggleEdit() {
      if (this.isEditing) {
        this.saveData(); // 保存数据
      }
      this.isEditing = !this.isEditing; // 切换编辑状态
    },
    saveData() {
      // 保存数据到 localStorage
      localStorage.setItem('username', this.username);
      localStorage.setItem('signature', this.signature);
      localStorage.setItem('phone', this.phone);
      localStorage.setItem('email', this.email);
      localStorage.setItem('qq', this.qq);
    },
    loadData() {
      // 从 localStorage 加载数据
      this.username = localStorage.getItem('username') || '用户名';
      this.signature = localStorage.getItem('signature') || '个性签名';
      this.phone = localStorage.getItem('phone') || '1234567890';
      this.email = localStorage.getItem('email') || 'example@example.com';
      this.qq = localStorage.getItem('qq') || '123456789';
      this.avatarUrl = localStorage.getItem('avatarUrl') || `https://api.adorable.io/avatars/80/${Math.random()}.png`; // 默认随机头像
    },
    loadJoinedProjects() {
      // 从 localStorage 加载项目经历
      const projects = JSON.parse(localStorage.getItem('joinedProjects')) || [];
      this.joinedProjects = projects;
    },
    loadCreatedProjects() {
      // 从 localStorage 加载创建的项目
      const projects = JSON.parse(localStorage.getItem('createdProjects')) || [];
      this.createdProjects = projects;
    },
  },
};
</script>

<style scoped>
.profile {
  padding: 20px;
  text-align: center;
  max-width: 400px; /* 限制最大宽度 */
  margin: auto; /* 居中 */
  border: 1px solid #ccc; /* 边框 */
  border-radius: 10px; /* 圆角 */
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1); /* 阴影 */
}

.header {
  display: flex;
  align-items: center;
  justify-content: flex-start; /* 左对齐 */
  margin-bottom: 20px;
}

.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background-color: #ccc;
  margin-right: 10px; /* 减小右边距 */
  background-size: cover; /* 使头像适应容器 */
}

.user-info {
  text-align: left; /* 左对齐 */
}

.user-info h2 {
  margin: 0; /* 去掉默认 margin */
}

.tabs {
  margin-bottom: 20px;
}

.tabs button {
  margin: 0 10px;
  padding: 10px 20px;
  cursor: pointer;
  background-color: #007bff; /* 按钮背景色 */
  color: white; /* 按钮文字颜色 */
  border: none; /* 去掉边框 */
  border-radius: 5px; /* 圆角 */
}

.content {
  margin-bottom: 20px;
  text-align: left; /* 左对齐 */
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

.edit-button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 5px; /* 圆角 */
}
</style>