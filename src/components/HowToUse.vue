<template>
    <div id="howToUse">
      <animationType v-if="!showContent" @startLearn="startLearn()" :numText="2"></animationType>
      <span  v-if="showContent" class="bigContainer">
          <section class="container"> 
              <figure v-for="(value, index) in arrText1" class="img-stack">
                <figcaption class="title">{{ titles1[index] }}</figcaption>
                  <figcaption class="text">{{ value }}</figcaption>
              </figure>
          </section>
          <section class="container"> 
              <figure v-for="(value, index) in arrText2" :key="i" class="img-stack">
                  <figcaption class="title">{{ titles2[index] }}</figcaption>
                  <figcaption class="text">{{ value }}</figcaption>
              </figure>
          </section>
      </span>
      <button v-if="showContent" @click="nextPage()"> המשך </button>
    </div>
  </template>

  <script>
  import AnimationType from './AnimationType.vue'
  export default {
    props: ['rightAns'],
    name: "howToUse",
    components: {AnimationType},
    data() {
      return {
        titles1: ["הדרגתיות","החלטיות","רגישות"],
        titles2: ["גיוון","אחידות ועקביות","התאמה"],
        arrText1: ["עלינו להתקדם במעלה החומרה של תגובתינו","ברגע שהחלטנו ע דרך פעולהת אין לפתוח זאת לדיון ולמיקוח","לא נעליב את החניך ונגלה רגישות למצב הכיתה ולצרכיה"],
        arrText2: ["ננסה לגוון את התגובות שלנו","נשתדל להגיב באותה מידה כלפי אותה התנהגות","יש להפעיל שיקול דעת בבחירת התגובה ולשים לב "],
        showContent: false
      }
    },
    methods: {
      nextPage() {
            this.$emit(`nextPage`,4);
        },
        startLearn() {
            this.showContent = true;
        }
    }
  }
  </script>
  
  
  <style scoped>

#howToUse {
  background-image: url("@/assets/artboard.svg");
  background-size: 100%, 100%;
  width: 100vw;
  height: 100vh;
  background-repeat: no-repeat;
  position: absolute;
  overflow: hidden;
  z-index: -2;
}

*, *::before, *::after {
  box-sizing: inherit;
  color: inherit;
}

.bigContainer {
    display: flex;
}

.container {
  position: relative;
  max-width: 50%;
  margin: 5em auto 0;
  display: flex;
  justify-content: center;
  min-height: 27em;
  border: 1px solid rgba(0, 0, 0, .1);
  direction: rtl;
}

.img-stack {
  position: absolute;
  padding: 1em;
  background: floralwhite;
  border: 1px solid #b9ab8e;
  border-radius: .1em;
  box-shadow: 0 2px 4px rgba(0, 0, 0, .3);
  transform-origin: center 325%; 
  transition: transform .5s ease-out;
  top: 10vh;
}

.container:hover .img-stack:first-child {
  transform: rotate(19deg);
}

.container:hover .img-stack:last-child {
  transform: rotate(-19deg);
}

.title{
  border-bottom: #3a3d40;
  font-size: 2vh;
}
  </style>