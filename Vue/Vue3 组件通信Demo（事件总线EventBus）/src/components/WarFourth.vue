<template>
  <div class="container">
    <div class="title">
      <div>我是0404</div>
    </div>
    <el-form label-width="auto">
      <el-form-item label="输入战情">
        <div class="input-group">
          <el-input v-model="postMsg"></el-input>
          <el-button @click="sendMessage" type="primary">发送</el-button>
        </div>
      </el-form-item>

      <el-form-item label="战绩汇总">
        <el-input
            disabled
            v-model="receivedMessage"
            :rows="10"
            type="textarea"
        />
      </el-form-item>
    </el-form>
  </div>
</template>

<script setup>
import {ref, onMounted, onBeforeUnmount} from 'vue';
import EventBus from '@/utils/EventBus';
import {dayjs} from 'element-plus'

const receivedMessage = ref('');
const postMsg = ref('');

const sendMessage = () => {
  EventBus.emit('custom-event', {message: postMsg.value});
  postMsg.value = ''
};

const handleCustomEvent = (payload) => {
  receivedMessage.value += dayjs().format('YYYY-MM-DD HH:mm:ss') + ' 0101战情：' + payload.message + '\n';
};

onMounted(() => {
  EventBus.on('custom-event', handleCustomEvent);
});

onBeforeUnmount(() => {
  EventBus.off('custom-event', handleCustomEvent);
});
</script>

<style scoped>
.container {
  padding: 20px;
}

.input-group {
  display: flex;
  align-items: center;
}

.input-group .el-input {
  flex: 1;
}

.input-group .el-button {
  margin-left: 8px;
}

.title {
  margin: 20px auto;
  font-weight: bold;
  text-align: center;
}
</style>