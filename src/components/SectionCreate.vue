<template>
  <v-form :class="classList" @submit.prevent="createSectionI">
    <v-text-field v-model="title" label="Add Item" type="text" class="input-text" v-on:focusin="startEditing" v-on:focusout="finishEditing">
    </v-text-field>
    
    <br>
     <v-btn class="mx-2" fab small dark color="indigo" v-if="isActive || titleExists" type="submit">
      <v-icon dark>
        mdi-plus
      </v-icon>
    </v-btn>
  </v-form>
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
