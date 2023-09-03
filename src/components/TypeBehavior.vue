<template>
  <div id="typeBehavior">
    <span class="typewriter"  v-if="!showContent">
      <h1>סוגי ההתנהגות של הלומדים,נלמד באמצעות משחק הזיכרון </h1>
      <button @click="startLearn()" > למד אותי </button>
    </span>
    <span class="cards" v-if="showContent">
      <div @click="checkAnswer(1, 0)" class="container" :class="cardClass[0]">
        <div>התנהגות אידיאלית</div>
      </div>
      <div @click="checkAnswer(3, 5)" class="container" :class="cardClass[5]">
      <div>התנהגות חריגה לגיטימית</div>
      </div>
      <div @click="checkAnswer(1, 1)" class="container" :class="cardClass[1]">
      <div>התנהגות מופתית, בהתאם לציפיות ודרישות המדדריך</div>
      </div>
      <div @click="checkAnswer(2, 2)" class="container" :class="cardClass[2]">
      <div>הפרעה ממשית</div>
      </div>
      <div @click="checkAnswer(4, 7)" class="container" :class="cardClass[7]">
      <div>התנהגות מכוונת שפוגעת בתהליך הלמידה ונובעת מסיבותיו האישיות של החניך (מוטיבציה, אופי, תקשורת וכו')</div>
      </div>
      <div @click="checkAnswer(2, 3)" class="container" :class="cardClass[3]">
      <div>התנהגות שפוגעת בתהליך הלמידה (בחניך או בסביבתו)</div>
      </div>
      <div @click="checkAnswer(4, 6)" class="container" :class="cardClass[6]">
      <div>התנגדות</div>
      </div>
      <div @click="checkAnswer(3, 4)" class="container" :class="cardClass[4]">
      <div>התנהגות שאינה פוגעת בתהליך הלמידה</div>
      </div>
  </span>
  <button @click="nextPage()" v-if="corrrectAnswer === 4 "> המשך </button>
  </div>
</template>

<script>
export default {
  props: ['rightAns'],
  name: "typeBehavior",
  data() {
    return {
        numOfTry: 0,
        lastAnswer: 0,
        ladtLocation: 0,
        cardClass: ["card", "card", "card", "card", "card", "card", "card", "card"],
        corrrectAnswer: 0,
        showContent: false
    }
  },
  methods: {
    checkAnswer(currentAnswer, location) {
      this.numOfTry++;
      if (this. numOfTry === 1){
        this.lastAnswer = currentAnswer;
        this.ladtLocation = location
      }
      else if (this. numOfTry === 2){
        this.numOfTry = 0;
        if (currentAnswer === this.lastAnswer && this.ladtLocation != location) {
          this.corrrectAnswer +=1;
          this.cardClass[location] +=  ` couple${currentAnswer}`;
          this.cardClass[this.ladtLocation] +=  ` couple${currentAnswer}`;
        }
        else {
          this.cardClass[location] += " shake";
          this.cardClass[this.ladtLocation] += " shake";
          setTimeout(() => {
            this.cardClass[location] = "card";
          this.cardClass[this.ladtLocation] = "card";
          }, 2000);
        }
      }
    },
    nextPage() {
      this.$emit(`nextPage`,3);
    },
    startLearn() {
            this.showContent = true;
    }
  },
}
</script>


<style scoped>
/* body {
  direction: rtl;
} */

.typewriter h1 {
  direction: rtl;
  color: black;
  font-family: monospace;
  overflow: hidden; 
  border-left: .15em solid; 
  white-space: nowrap; 
  /* margin: 0 auto; */
  letter-spacing: .15em; 
  animation: 
    typing 3.5s steps(30, end),
    blink-caret .5s step-end infinite;
}

/* The typing effect */
@keyframes typing {
  from { width: 0 }
  to { width: 30% }
}


@keyframes blink-caret {
  from, to { border-color: transparent }
  50% { border-color: black }
}
.card {
  width: 10vw;
  height: 15vw;
  background-color: black;
  border-radius: 5%;
  cursor: pointer;
  padding: 3px;
  position: relative;
  color: white;

  

}
.container{
  display: flex;
  direction: rtl;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;

}
.cards {
  margin-top: 15vh;
  margin-left: 25vw;
  display: flex;
  width: 49vw;
  height: 60vh;
  flex-wrap: wrap;
  justify-content: space-between;
}


.couple1::before {
  content: "";
  width: 104%;
  height: 102%;
  border-radius: 8px;
  background-image: linear-gradient(
    var(--rotate)
    , #5ddcff, #3c67e3 43%, #4e00c2);
    position: absolute;
    z-index: -1;
    top: -1%;
    left: -2%;
    animation: spin 2.5s linear infinite;
}

.couple1::after {
  position: absolute;
  content: "";
  top: calc(var(--card-height) / 6);
  left: 0;
  right: 0;
  z-index: -1;
  height: 100%;
  width: 100%;
  margin: 0 auto;
  transform: scale(0.8);
  filter: blur(calc(var(--card-height) / 6));
  background-image: linear-gradient(
    var(--rotate)
    , #5ddcff, #3c67e3 43%, #4e00c2);
    opacity: 1;
  transition: opacity .5s;
  animation: spin 2.5s linear infinite;
}

.couple2::before {
  content: "";
  width: 104%;
  height: 102%;
  border-radius: 8px;
  background-image: linear-gradient(
    var(--rotate)
    , #ffb3d1,#ff66a3 43%, #ff3385);
    position: absolute;
    z-index: -1;
    top: -1%;
    left: -2%;
    animation: spin 2.5s linear infinite;
}

.couple2::after {
  position: absolute;
  content: "";
  top: calc(var(--card-height) / 6);
  left: 0;
  right: 0;
  z-index: -1;
  height: 100%;
  width: 100%;
  margin: 0 auto;
  transform: scale(0.8);
  filter: blur(calc(var(--card-height) / 6));
  background-image: linear-gradient(
    var(--rotate)
    , #ffb3d1,#ff66a3 43%, #ff3385);
    opacity: 1;
  transition: opacity .5s;
  animation: spin 2.5s linear infinite;
}

.couple3::before {
  content: "";
  width: 104%;
  height: 102%;
  border-radius: 8px;
  background-image: linear-gradient(
    var(--rotate)
    ,  #ffc299,#ff8533 43%, #ff6600);
    position: absolute;
    z-index: -1;
    top: -1%;
    left: -2%;
    animation: spin 2.5s linear infinite;
}

.couple3::after {
  position: absolute;
  content: "";
  top: calc(var(--card-height) / 6);
  left: 0;
  right: 0;
  z-index: -1;
  height: 100%;
  width: 100%;
  margin: 0 auto;
  transform: scale(0.8);
  filter: blur(calc(var(--card-height) / 6));
  background-image: linear-gradient(
    var(--rotate)
    , #ffc299,#ff8533 43%, #ff6600);
  opacity: 1;
  transition: opacity .5s;
  animation: spin 2.5s linear infinite;
}

.couple4::before {
  content: "";
  width: 104%;
  height: 102%;
  border-radius: 8px;
  background-image: linear-gradient(
    var(--rotate)
    , #ffffb3, #ffff4d 43%, #e6e600);
    position: absolute;
    z-index: -1;
    top: -1%;
    left: -2%;
    animation: spin 2.5s linear infinite;
}

.couple4::after {
  position: absolute;
  content: "";
  top: calc(var(--card-height) / 6);
  left: 0;
  right: 0;
  z-index: -1;
  height: 100%;
  width: 100%;
  margin: 0 auto;
  transform: scale(0.8);
  filter: blur(calc(var(--card-height) / 6));
  background-image: linear-gradient(
    var(--rotate)
    , #ffffb3, #ffff4d 43%, #e6e600);
  opacity: 1;
  transition: opacity .5s;
  animation: spin 2.5s linear infinite;
}

.shake{
  animation: shake 1s 
  
  
  
  
  
  ;
}

@keyframes spin {
  0% {
    --rotate: 0deg;
  }
  100% {
    --rotate: 360deg;
  }
}

@keyframes shake {
  0% {
    transform:  rotate(5deg);
  }
  25% {
    transform:  rotate(-5deg);
  }
  50% {
    transform:  rotate(2deg);
  }
  75% {
    transform:  rotate(-5deg);
  }
  100% {
    transform: rotate(-2deg);
  }
}

</style>

@keyframes shake {
  0% {
    transform: scale(1);
  }

  30% {
    transform: scale(1.35);
  }
  45% {
    transform: scale(1.35) rotate(5deg);
  }
  60% {
    transform: scale(1.35) rotate(-5deg);
  }
  70% {
    transform: scale(1.35) rotate(2deg);
  }
  80% {
    transform: scale(1.35) rotate(-5deg);
  }
  95% {
    transform: scale(1.35) rotate(-2deg);
  }
  100% {
    transform: scale(1.35);
  }
}