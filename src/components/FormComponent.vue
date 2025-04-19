<template>
  <div class="form-container">
    <h2>用户信息表单</h2>
    <form @submit.prevent="handleSubmit">
      <div class="form-group">
        <label for="name">姓名:</label>
        <input 
          type="text" 
          id="name" 
          v-model="formData.name" 
          required 
          placeholder="请输入您的姓名"
        >
      </div>
      
      <div class="form-group">
        <label for="email">邮箱:</label>
        <input 
          type="email" 
          id="email" 
          v-model="formData.email" 
          required 
          placeholder="请输入您的邮箱"
        >
      </div>
      
      <div class="form-group">
        <label for="phone">电话:</label>
        <input 
          type="tel" 
          id="phone" 
          v-model="formData.phone" 
          placeholder="请输入您的电话号码"
        >
      </div>
      
      <div class="form-group">
        <label for="message">留言:</label>
        <textarea 
          id="message" 
          v-model="formData.message" 
          rows="4" 
          placeholder="请输入您的留言"
        ></textarea>
      </div>
      
      <button type="submit" :disabled="isSubmitting">
        {{ isSubmitting ? '提交中...' : '提交' }}
      </button>
    </form>
    
    <div v-if="submitStatus" class="status-message" :class="{ 'success': submitStatus === 'success', 'error': submitStatus === 'error' }">
      {{ statusMessage }}
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const formData = ref({
  name: '',
  email: '',
  phone: '',
  message: ''
});

const isSubmitting = ref(false);
const submitStatus = ref(null);
const statusMessage = ref('');

const handleSubmit = async () => {
  isSubmitting.value = true;
  submitStatus.value = null;
  
  try {
    // 这里模拟API调用，实际项目中替换为真实的API请求
    await submitFormData(formData.value);
    
    submitStatus.value = 'success';
    statusMessage.value = '表单提交成功！';
    
    // 清空表单
    formData.value = {
      name: '',
      email: '',
      phone: '',
      message: ''
    };
  } catch (error) {
    submitStatus.value = 'error';
    statusMessage.value = '提交失败，请稍后重试。';
    console.error('提交错误:', error);
  } finally {
    isSubmitting.value = false;
  }
};

// 模拟API提交函数
const submitFormData = (data) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      // 模拟随机成功/失败
      const isSuccess = Math.random() > 0.2;
      if (isSuccess) {
        console.log('提交的数据:', data);
        resolve();
      } else {
        reject(new Error('服务器错误'));
      }
    }, 1000);
  });
};
</script>

<style scoped>
.form-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  color: #333;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

input, textarea {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
}

textarea {
  resize: vertical;
}

button {
  background-color: #4CAF50;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background-color: #45a049;
}

button:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}

.status-message {
  margin-top: 15px;
  padding: 10px;
  border-radius: 4px;
}

.success {
  background-color: #dff0d8;
  color: #3c763d;
}

.error {
  background-color: #f2dede;
  color: #a94442;
}
</style>