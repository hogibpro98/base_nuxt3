<template>
  <div style="background: red">
    <h1>red</h1>
    <button @click="onChildClick">Call Child's Increment Method</button>
    <p>its child component</p>
    <ChildComponent ref="child" />
    <p>Child's Count: {{ childCount }}</p>
    // new Ex
    <div>
      <h3>Ex:</h3>
      <span>{{ cloneData }}</span>
      <button @click="callList">callList</button>
      <ex ref="exRef" :custom-loading="isLoading"></ex>
    </div>
  </div>
</template>

<script setup>
import ChildComponent from '~/component/defineExpose/childComponent.vue';
import ex from '@/component/defineExpose/ex.vue';
import { ref } from 'vue';

const child = ref(null)
const childCount = ref(0)
const isLoading = ref(false);

const onChildClick = () => {
  child.value.increment()
}

// new Ex
const cloneData = ref([]);
const exRef = ref(null)
const callList = () => {
  isLoading.value = true;
  exRef.value.reset()
}
onMounted(() => {
  childCount.value = child.value.count;
  // new Ex
  cloneData.value = exRef.value.todos;
  isLoading.value = exRef.value.state.isLoading;
})
</script>
