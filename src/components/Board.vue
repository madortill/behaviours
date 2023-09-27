<template>
    <div id="board">
        <span v-if="!showContent">
            <div>{{ arrText[numPage] }}</div>
            <button @click="startLearn()" > למד אותי </button>
        </span>
        <span v-if="showContent">
        <typeBehavior @nextPage="changePage" v-if="numPage === 0" ></typeBehavior>
        <comments @nextPage="changePage" v-if="numPage === 1"></comments>
        <howToUse @nextPage="changePage" v-if="numPage === 2"></howToUse>
        </span>
    </div>
  </template>

  <script>
import TypeBehavior from './TypeBehavior.vue'
import HowToUse from './HowToUse.vue'
import Comments from './Comments.vue'
export default {
    components: {TypeBehavior,HowToUse,Comments},
    name: "board",
    data() {
      return {
          arrText: ["סוגי ההתנהגות של הלומדים,נלמד באמצעות משחק הזיכרון", "תגובות אפשריות של המדריך", "עקרונות לבחירה ושימוש בתגובה"],
          numPage: 0,
          showContent: false
      }
    },
    methods: {
        changePage(thePage) {
            if(thePage === 2) {
                this.$emit(`nextPage`,1);
            }
            this.showContent = false;
            this.numPage = thePage;
        },

        startLearn() {
            this.showContent = true;
        }
    }
  }
  </script>
  
  
  <style scoped>
  
  </style>