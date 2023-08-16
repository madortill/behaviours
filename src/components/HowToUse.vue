<template>
    <div id="howToUse">
      <span v-if="!showContent">
            <div>עקרונות לבחירה ושימוש בתגובה</div>
            <button @click="startLearn()" > למד אותי </button>
      </span>
      <span  v-if="showContent" class="bigContainer">
          <section class="container"> 
              <figure v-for="i in arrText1" class="img-stack">
                  <div>{{ arrText1[i] }}</div>
                  <figcaption class="img-stack__caption">Waterfall in Dundas Peak, Ontario, Canada </figcaption>
              </figure>
          </section>
          <section class="container"> 
              <figure v-for="i in arrText2" class="img-stack">
                  <div>{{ arrText2[i] }}</div>
                  <figcaption class="img-stack__caption">Waterfall in Dundas Peak, Ontario, Canada </figcaption>
              </figure> 
          </section>
      </span>
      <button @click="nextPage()"> המשך </button>
    </div>
  </template>

  <script>
  export default {
    props: ['rightAns'],
    name: "howToUse",
    data() {
      return {
        arrText1: ["","",""],
        arrText2: ["","",""],
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

HTML {
  font-family: "Libre Baskerville", "Open Sans", sans-serif, serif;
  font-size: 100%;
  line-height: 1.5;
  box-sizing: border-box;
}

BODY {
  color: #3a3d40;
}

*, *::before, *::after {
  box-sizing: inherit;
  color: inherit;
}

IMG { max-width: 100%; }

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
}

/*Actual Style*/

.img-stack {
  position: absolute;
  padding: 1em;
  background: floralwhite;
  border: 1px solid #b9ab8e;
  border-radius: .1em;
  box-shadow: 0 2px 4px rgba(0, 0, 0, .3);
  transform-origin: center 325%; 
  transition: transform .5s ease-out;
}

.img-stack__image {
  max-width: 500px;
}

.img-stack:first-child {
  transform: rotate(1deg);
}

.img-stack:last-child {
  transform: rotate(-1deg);
}

.container:hover .img-stack:first-child {
  transform: rotate(19deg);
}

.container:hover .img-stack:last-child {
  transform: rotate(-19deg);
}

.img-stack:hover {
  z-index: 1;
}

  </style>