<template>
  <form :class="classList" @submit.prevent="createSectionI">
    <input v-model="title" type="text" class="input-text" placeholder="Add Item" @focusin="startEditing" @focusout="finishEditing"/>
    <br>
    <button v-if="isActive || titleExists" type="submit" class="add-button">➕</button>
  </form>
</template>

<script>

import { mapActions } from 'vuex'

export default{
  data(){
    return {
      title: '',
      isActive: false,
    }
  },
  computed: {
    classList(){
      let classList = ['addSection'];
      if(this.isActive){
        classList.push('active');
      }
      return classList;
    }, 
    titleExists(){
      return this.title.length > 0;
    },
  },
  methods: {
    ...mapActions(["createSection"]),
    createSectionI(){
      this.createSection({ title: this.title});
      this.title = '';
    },
    startEditing(){
      this.isActive = true;
    },
    finishEditing(){
      this.isActive = false;
    },
  },
}
</script>