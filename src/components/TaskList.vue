<template>
  <div class="blocker d-flex gap-4 flex-wrap mt-5 align-items-center justify-content-center">
    <TaskCard 
      v-for="(task, index) in list" 
      :key="index"
      :task="task"
      :index="index"
      @completed="completeFn"
      @delete="$emit('delete', index)"
      @edit="$emit('edit', [index, true])"
    />
  </div>
</template>

<script setup>
import TaskCard from './TaskCard.vue';
import { defineProps ,defineEmits } from "vue"
  defineProps({
    list: Array
  })
  const emits = defineEmits(['delete','completed','edit'])
  const completeFn = (params) => {
    const [index, complete] = params
    emits('completed',[index, complete])
  }
</script>

<!-- Same but with Options API -->
<!-- 
  <script>
import TaskCard from './TaskCard.vue';
export default {
  name: "TaskList",
  props: [
    'list'
  ],
  components: {
    TaskCard
  },
  emits: ['delete','completed','edit'],
  methods: {
    completeFn(params){
      const [index, complete] = params
      this.$emit('completed',[index, complete])
    }
  }
};
</script>
 -->

<style scoped>
  @media(max-width:900px){
    .blocker {
      display: block !important;
    }
  }
</style>
