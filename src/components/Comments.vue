<template>
    <div id="comments">
      <animationType v-if="!showContent" @startLearn="startLearn()" :numText="1"></animationType>
      <div v-if="showContent" class="container">
          <div id="stack" class="slider" >
              <div :key="slide.index" v-for="(slide, i) in slides" @click="moveSlide()" class="slide">
                  <div :class="animation > 0 ? `slide__inner animation` : `slide__inner`" > {{slide.name}} 
                      <div class="text"> {{slide.description}} </div>
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
                'description': "גורמת לחניך לחוש מחויבות לשיעור"
            },
            {
                'index': 2,
                'name': "שתיקה",
                'description': "מנוגדת להתנהגות הרגילה של המדריך, ולכן מרכזת את תשומת לב החניכים"
            },
            {
                'index': 3,
                'name': "שיקוף",
                'description': "שיקוף מילולי- תיאור התנהגות אובייקטיבי, שיקוף השלכות- תיאור ההשלכות של ההתנהגות על החניך עצמו, המדריך או הכיתה כולה"
            },
            {
                'index': 4,
                'name': "סילוק גורמים מסיחים",
                'description': "גורם מסיח הינו חפץ נייח או חניך שמפריע, יש לציין מתי החפץ יוחזר ולמקמו במקום ידוע לחניך"
            },
            {
                'index': 5,
                'name': "הומור",
                'description': "הומור יוצר אווירה לימודית נעימה ומשוחררת, מעודד ומעורר מוטיבציה וקשב יש להזהר מהערות פוגעות ומעליבות"
            },
            {
                'index': 6,
                'name': "הגדרת חוזה התנהגותי",
                'description': "מהווה הבהרה מחדש של כללי ההתנהגות, שימושי כשדפוס התנהגות מסוים משתרש בכיתה כולה"
            },
            {
                'index': 7,
                'name': "סילוק ידידותי",
                'description': "אין להביע כעס! על החניך להבין שהדבר נעששה לטובתו ולטובת כל הכיתה, יש להגדיר לחניך היכן להימצא, מה לעשות ומתי לחזור לכיתה"
            },
            {
                'index': 8,
                'name': "חיובי",
                'description': "אם ניטול את האפי השלילי של התגובה ונתייחס אליה כאל תגובה רצויה וחיובית- היא אכן תהפוך לכזו"
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
.text {
  position: absolute;
  text-align: center;
  direction: rtl;
  width: 13vw;
  margin-right: 10%;
  margin-top: 45%;
  font-size: 1vw;
}
  
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
  margin-top: 13vh;
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
  background-color: #ffd580;
  border: 0.2vh solid #ffad33;
  display: flex;
  position: relative;;
}

.slide {
  width: 100%;
  height: 100%;
  position: absolute;
  cursor: pointer;
  background-color: #ffd580;
  border: 0.2vh solid #ffad33;
  transition: transform 100ms ease-in-out;
  margin-left: 5%;
  margin-top: 5%;
  
 
}


.slide__inner {
  background-color: #ffd580;
  border: 0.2vh solid #ffad33;
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 100ms ease-in-out;
  background-size: cover;
  margin-top: 5%;
  margin-left: 5%;
  text-align: center;
  direction: rtl;
  font-size: 1.5vw;
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

