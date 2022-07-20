<template>
  <v-form v-bind:class="classList" v-on:submit.prevent="createTaskInSectionI">
    <v-text-field v-model="content" label="Add Task" type="text" class="input-text" v-on:focusin="startEditing" v-on:focusout="finishEditing">
    </v-text-field>
   <br>
    <v-btn class="mx-2" fab small dark color="indigo" v-if="isActive || contentExists" type="submit">
      <v-icon dark>
        mdi-plus
      </v-icon>
    </v-btn>
  </v-form>
</template>

<script>

import { mapActions } from 'vuex'

export default{
  props:{
    sectionIndex: {
      type: Number,
      required: true,
    }
  },
  data(){
    return {
      content: '',
      isActive: false,
    }
  },
  computed: {
    classList(){
      let classList = []
      if(this.isActive){
        classList.push('active')
      }
      return classList
    },
    contentExists(){
      return this.content.length > 0;
    },
  },
  methods:{
    ...mapActions(["createTaskInSection"]),
    createTaskInSectionI(){
      //console.log(this.content);
      this.createTaskInSection({ content: this.content, sectionIndex: this.sectionIndex });
      this.content = '';
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

