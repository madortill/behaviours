<template>
    <div id="comments">
      <!-- <span class="typewriter" v-if="!showContent">
            <h1>תגובות אפשריות של המדריך</h1>
            <button @click="startLearn()" > למד אותי </button>
      </span> -->
      <animationType v-if="!showContent" @startLearn="startLearn()" :numText="1"></animationType>
      <div v-if="showContent" class="container">
          <div id="stack" class="slider" >
              <div :key="slide.index" v-for="(slide, i) in slides" @click="moveSlide()" class="slide">
                  <div :class="animation > 0 ? `slide__inner animation` : `slide__inner`" > {{slide.name}} 
                      <div > {{slide.description}} </div>
                    </div>
              </div>
          </div>
      </div>
      <button class="next" @click="nextPage()" v-if="animation  >= 8"> המשך </button>
    </div>
  </template>

  <script>
  import AnimationType from './AnimationType.vue'
  export default {
    props: ['rightAns'],
    name: "comments",
    components: {AnimationType},
    data() {
        return {
            slides: [
            {
                'index': 0,
                'name': "מבט",
                'description': "ישר ורציני לעני החניך, משמש כתגובה להפרעות קלות"
            },
            {
                'index': 1,
                'name': "קרבה פיזית",
                'description': "ישר ורציני לעני החניך, משמש כתגובה להפרעות קלות"
            },
            {
                'index': 2,
                'name': "שתיקה",
                'description': "ישר ורציני לעני החניך, משמש כתגובה להפרעות קלות"
            },
            {
                'index': 3,
                'name': "שיקוף",
                'description': "ישר ורציני לעני החניך, משמש כתגובה להפרעות קלות"
            },
            {
                'index': 4,
                'name': "סילוק גורמים מסיחים",
                'description': "ישר ורציני לעני החניך, משמש כתגובה להפרעות קלות"
            },
            {
                'index': 5,
                'name': "הומור",
                'description': "ישר ורציני לעני החניך, משמש כתגובה להפרעות קלות"
            },
            {
                'index': 6,
                'name': "הגדרת חוזה התנהגותי",
                'description': "ישר ורציני לעני החניך, משמש כתגובה להפרעות קלות"
            },
            {
                'index': 7,
                'name': "סילוק ידידותי",
                'description': "ישר ורציני לעני החניך, משמש כתגובה להפרעות קלות"
            },
            {
                'index': 8,
                'name': "חיובי",
                'description': "ישר ורציני לעני החניך, משמש כתגובה להפרעות קלות"
            }
            ],
            animation: 0,
            showContent: false
        }
    },

    methods: {
        moveSlide() {
            this.animation +=1;
            this.slides.unshift(this.slides.pop())
        },

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
  #comments {
  background-image: url("@/assets/artboard.svg");
  background-size: 100%, 100%;
  width: 100vw;
  height: 100vh;
  background-repeat: no-repeat;
  position: absolute;
  z-index: -2;
}

.next {
  display: block;
  margin: 0 auto;
  margin-top: 2vh;
}

.container {
  width: 60vw;
  height: 60vh;
  margin-top: 20vh;
  margin-left: 20vw;
  display: flex;

}

.slider {
  width: 300px;
  height: 450px;
  margin: 0 auto;
  border: 0.2vh solid black;
  background-color: #2968b6;
  display: flex;
  position: relative;;
}

.slide {
  width: 100%;
  height: 100%;
  position: absolute;
  cursor: pointer;
  border: 0.2vh solid black;
  background-color: #2968b6;
  transition: transform 100ms ease-in-out;
  margin-left: 5%;
  margin-top: 5%;
  /* animation: slide 1s linear; */
 
}
/* .slider--loaded:nth-child(2)  {
  transform: translate3d(-20px, -20px, 0)
}

.slider--loaded:nth-child(3) {
  transform: translate3d(-40px, -40px, 0)
}

.slider--loaded:nth-child(4) {
  transform: translate3d(-60px, -60px, 0)
} */

.slide__inner {
  background-color: #2968b6;
  border: 0.2vh solid black;
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 100ms ease-in-out;
  background-size: cover;
  margin-top: 5%;
  margin-left: 5%;
  /* animation: slide 1s linear; */
}

.animation{
    animation: slide 1s linear;
}

.slide:nth-child(9) .slide__inner:hover {
  transform: scale(1.02);
}

@keyframes slide {
  0% {
    transform: translate3d(0px, 0px, 0px)
  }
  40%{
    transform: translate3d(-40px, -40px, 0)
  }
  80% {
    transform: translate3d(-60px, -60px, 0)
  }
  100%{
    transform: translate3d(0px, -60px, 0)
  }
}
  </style>

