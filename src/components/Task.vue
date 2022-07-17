<template>
  <div :class="classList">
    <button class="delete-button" @click="deleteTaskI" type="primary">❌</button>
    <button class="edit-button" @click="updateTaskI" type="primary">✏️</button>
    <h3 v-if="!isEditing">{{ this.task.content }}</h3>
    <div v-else>
      <input :value="newContent" @change="taskContentChange" type="text" class="input-task"/>
    </div>
    
  </div>
</template>

<script>

import { mapActions } from 'vuex'

export default{
  props: {
    sectionIndex: {
      type: Number,
      required: true
    },
    taskIndex: {
      type: Number,
      required: true
    },
    task: {
      type: Object,
      required: true
    },
  },
  data(){
    return {
      newContent: "",
      isEditing: false,
    }
  },
  computed: {
    classList(){
      const classList = ['task']
      return classList;
    },
  },
  methods:{
    ...mapActions(['deleteTask', 'updateTask']),
    deleteTaskI(){
      if(confirm("Do you really want to delete this task?")){
        this.deleteTask({ taskIndex: this.taskIndex, sectionIndex: this.sectionIndex })
      }
      else return;
    },
    taskContentChange(e){
      this.newContent = e.target.value;
    },
    updateTaskI(){
      console.log(this.task.content);
      this.isEditing = this.isEditing == true ? false : true;
      if(this.isEditing){
        this.newContent = this.task.content;
        this.updateTask(this.task);
      }
      else{
        this.task.content = this.newContent;
      }
    }
  },
}
</script>

<style>
.task {
  margin: 10px 0;
  position: relative;
  padding: 20px 15px;
  background-color: rgba(37, 36, 36, 0.712);
  border-radius: 10px;
  width: 260px;
  cursor: pointer;
}

.delete-button {
  position: absolute;
  top: 5px;
  right: 5px;
  font-size: 20px;
  cursor: pointer;
  border-radius: 8px;
  border: none;
  margin: 5px;
}

.delete-button:hover{
  opacity: 0.8;
  cursor: pointer;
}

.edit-button{
  position: absolute;
  padding: 5px 8px;
  bottom: 5px;
  right: 5px;
  font-size: 15px;
  cursor: pointer;
  border-radius: 10px;
  border: none;
  margin: 5px;
}

.edit-button:hover{
  opacity: 0.8;
  cursor: pointer;
}

.content {
  font-size: 20px;
}

</style>