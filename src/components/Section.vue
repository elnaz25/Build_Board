<template>
  <div class="section">
    <div class="listheader">
      <p class="section-title">{{ title }}</p>
      <div class="deleteSection" @click="deleteSectionI">×</div>
    </div>
    <draggable group="tasks" :list="tasks" @end="$emit('change')">
      <Task v-for="(task, index) in tasks" :key="task.id" :task="task" :taskIndex="index" :sectionIndex="sectionIndex"/>
      <br>
      <TaskCreate :sectionIndex="sectionIndex"/>
    </draggable>
  </div>
</template>

<script>

import TaskCreate from './TaskCreate.vue'
import Task from './Task.vue'
import draggable from 'vuedraggable'
import { mapActions } from 'vuex'

export default{
  components: {
    TaskCreate,
    Task,
    draggable,
  },
  props: {
    title: {
      type: String,
      required: true
    },
    tasks: {
      type: Array,
      required: true
    },
    sectionIndex: {
      type: Number,
      required: true
    },
  },
  methods: {
    ...mapActions(["deleteSection"]),
    deleteSectionI(){
      this.deleteSection({sectionIndex: this.sectionIndex});
    },
  }
}
</script>