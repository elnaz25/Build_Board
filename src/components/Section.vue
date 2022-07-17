<template>
  <div class="section">
    <div class="listheader">
      <p class="section-title">{{ title }}</p>
      <div class="deleteSection" @click="deleteSectionI">×</div>
    </div>
    <draggable group="tasks" :list="tasks" @end="$emit('change')">
      <Task v-for="(task, index) in tasks" :key="task.id" :task="task" :taskIndex="index" :sectionIndex="sectionIndex"/>
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

<style>
.addSection {
  margin: 0 10px;
  padding: 12px;
  display: inline-block;
  flex-direction: column;
  align-items: flex-start;
  border-radius: 120px;
  font-weight: 500;
  font-size: 15px;
}

.deleteSection {
  position: absolute;
  top: 3px;
  right: 10px;
  font-size: 25px;
}

.deleteSection:hover {
  opacity: 0.8;
  cursor: pointer;
}

.section {
  margin: 0 5px auto;
  position: relative;
  display: inline-block;
  flex-direction: column;
  align-items: flex-start;
  width: 290px;
  background-color: #0c0c0ca6;
  border-radius: 10px;
  padding: 15px;
  border: solid rgb(243, 243, 243) 1px;
  color: rgb(253, 252, 252);
  vertical-align: top;
  overflow-y: scroll;
}

.section-title {
  font-size: 25px;
  font-weight: bold;
}

</style>