<template>
  <div :class="classList">

    <v-btn class="delete-button" type="primary" fab dark small @click="deleteTaskI">
      <v-icon dark>
        mdi-delete
      </v-icon>
    </v-btn>

    <v-btn class="edit-button" type="primary" fab dark small @click="updateTaskI">
      <v-icon dark>
        mdi-pencil
      </v-icon>
    </v-btn>

    <h3 v-if="!isEditing">{{ this.task.content }}</h3>
    <div v-else>
      <v-text-field :value="newContent" @change="taskContentChange" type="text" class="input-task"></v-text-field>
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
      //console.log(this.task.content);
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

