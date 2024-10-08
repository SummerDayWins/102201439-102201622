<template>
  <view class="container">
    <view class="search-bar">
      <input 
        v-model="searchQuery" 
        placeholder="搜索项目" 
        class="search-input" 
        @keyup.enter="searchProjects" 
      />
    </view>
    <text class="title">加入项目</text>
    <view class="project-list">
      <view class="project-card" v-for="project in filteredProjects" :key="project.id">
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
        <button 
          class="apply-button" 
          :disabled="project.joined" 
          @click="applyForProject(project.id)" 
          v-if="!project.joined"
        >
          申请加入
        </button>
        <button 
          class="joined-button" 
          v-else
        >
          已加入
        </button>
      </view>
    </view>
    <button class="my-projects-button" @click="goToMyProjects">我加入的项目</button>
  </view>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
      projects: [
        {
          id: 1,
          name: '智能助手开发',
          description: '这是一个关于人工智能的项目，旨在开发智能助手，帮助用户提高工作效率。',
          avatarUrl: 'https://picsum.photos/80/80?random=1',
          tags: ['人工智能', '助手'],
          joined: false,
        },
        {
          id: 2,
          name: '区块链应用探索',
          description: '本项目专注于区块链技术的应用，探索去中心化的解决方案。',
          avatarUrl: 'https://picsum.photos/80/80?random=2',
          tags: ['区块链', '去中心化'],
          joined: false,
        },
        {
          id: 3,
          name: '健康管理系统',
          description: '这是一个关于健康管理的项目，旨在通过数据分析帮助用户改善生活方式。',
          avatarUrl: 'https://picsum.photos/80/80?random=3',
          tags: ['健康', '数据分析'],
          joined: false,
        },
        {
          id: 4,
          name: '在线教育平台',
          description: '这是一个关于教育的项目，旨在提供在线学习资源，帮助学生提高学习效率。',
          avatarUrl: 'https://picsum.photos/80/80?random=4',
          tags: ['教育', '在线学习'],
          joined: false,
        },
        {
          id: 5,
          name: '可持续发展倡议',
          description: '本项目致力于环境保护，推动可持续发展，提升公众环保意识。',
          avatarUrl: 'https://picsum.photos/80/80?random=5',
          tags: ['环境', '可持续发展'],
          joined: false,
        },
      ],
    };
  },
  mounted() {
    this.loadJoinedProjects(); // 加载已加入的项目状态
  },
  computed: {
    filteredProjects() {
      return this.projects.filter(project => 
        project.name.includes(this.searchQuery) || 
        project.tags.some(tag => tag.includes(this.searchQuery))
      );
    },
  },
  methods: {
    searchProjects() {
      console.log(`Searching for: ${this.searchQuery}`);
    },
    applyForProject(projectId) {
      const project = this.projects.find(p => p.id === projectId);
      if (project) {
        project.joined = true; // 设置为已加入
        this.saveJoinedProject(project); // 保存到本地存储
        uni.showToast({ title: `已申请加入项目: ${project.name}`, icon: 'success' });
      }
    },
    saveJoinedProject(project) {
      let joinedProjects = JSON.parse(localStorage.getItem('joinedProjects')) || [];
      
      // 检查项目是否已经存在
      const exists = joinedProjects.some(p => p.id === project.id);
      if (!exists) {
        joinedProjects.push(project);
        localStorage.setItem('joinedProjects', JSON.stringify(joinedProjects));
      }
    },
    loadJoinedProjects() {
      const joinedProjects = JSON.parse(localStorage.getItem('joinedProjects')) || [];
      joinedProjects.forEach(joinedProject => {
        const project = this.projects.find(p => p.id === joinedProject.id);
        if (project) {
          project.joined = true; // 更新项目状态为已加入
        }
      });
    },
    goToMyProjects() {
      uni.navigateTo({ url: '/pages/myProjects/myProjects' });
    },
  },
};
</script>

<style>
.container {
  padding: 20px;
}

.search-bar {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.search-input {
  width: 80%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
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

.apply-button {
  width: 100%;
  padding: 10px;
  background-color: #28a745; /* 绿色 */
  color: white;
  border: none;
  border-radius: 5px;
  margin-top: 10px;
}

.joined-button {
  width: 100%;
  padding: 10px;
  background-color: #6c757d; /* 灰色 */
  color: white;
  border: none;
  border-radius: 5px;
  margin-top: 10px;
}

.my-projects-button {
  width: 100%;
  padding: 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  text-align: center;
}
</style>