<template>
  <div class="profile">
    <div class="header">
      <div class="avatar">头像</div>
      <div class="user-info">
        <h2>用户名</h2>
        <p>个性签名</p>
        <p>电话：{{ phone }}</p>
        <p>邮箱：{{ email }}</p>
        <p>QQ：{{ qq }}</p>
      </div>
    </div>
    <div class="tabs">
      <button @click="showEducation = true">教育经历</button>
      <button @click="showEducation = false">项目经历</button>
    </div>
    <div class="content">
      <div v-if="showEducation">
        <h3>教育经历</h3>
        <p>就读专业：xxxxxxxxx</p>
        <p>已修：xxxxxxxxx</p>
        <p>专业技能：xxxxxxxxx</p>
      </div>
      <div v-else>
        <h3>项目经历</h3>
        <p>项目名称：xxxxxxxxx</p>
        <p>项目描述：xxxxxxxxx</p>
        <p>使用技术：xxxxxxxxx</p>
      </div>
    </div>
    <button class="edit-button">编辑</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showEducation: true, // 默认显示教育经历
      phone: '1234567890',
      email: 'example@example.com',
      qq: '123456789',
    };
  },
};
</script>

<style scoped>
.profile {
  padding: 20px;
  text-align: center;
}

.header {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
}

.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background-color: #ccc;
  margin-right: 20px;
}

.tabs {
  margin-bottom: 20px;
}

.tabs button {
  margin: 0 10px;
  padding: 10px 20px;
  cursor: pointer;
}

.content {
  margin-bottom: 20px;
}

.edit-button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}
</style>