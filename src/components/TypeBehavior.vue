<template>
  <div id="typeBehavior">
    <animationType v-if="!showContent" @startLearn="startLearn()" :numText="0"></animationType>
    <span class="cards" v-if="showContent">
      <div v-for="(key, index) in shuffleKeys" @click="checkAnswer(index, answers[key])" :class="['card', cardClass[index]]"  :key='key' :ref="'card ' + index" @animationend="removeShake">
        <div> {{ key }} </div>
      </div>
    </span>
    <button class="next" @click="nextPage()" v-if="corrrectAnswer === 4"> המשך </button>
  </div>
</template>

<script>
import AnimationType from './AnimationType.vue'
export default {
  props: ['rightAns'],
  name: "typeBehavior",
  components: { AnimationType },
  data() {
    return {
      numOfTry: 0,
      lastAnswer: 0,
      ladtLocation: 0,
      cardClass: ["card", "card", "card", "card", "card", "card", "card", "card"],
      corrrectAnswer: 0,
      showContent: false,
      pressed: false,
      answers: // term: definition
      {
        'התנהגות אידיאלית': 0,
        'התנהגות מופתית, בהתאם לציפיות ודרישות המדריך': 0,
        'התנהגות חריגה לגיטימית': 1,
        'התנהגות שאינה פוגעת בתהליך הלמידה': 1,
        'הפרעה ממשית': 2,
        'התנהגות שפוגעת בתהליך הלמידה (בחניך או בסביבתו)': 2,
        'התנגדות': 3,
        'התנהגות מכוונת שפוגעת בתהליך הלמידה ונובעת מסיבותיו האישיות של החניך (מוטיבציה, אופי, תקשורת וכו\')': 3
      }
    }
  },
  methods: {
    checkAnswer(location, currentAnswer) {
      if (!this.cardClass[location].includes("couple")) {
        if (this.numOfTry === 0) {
          this.lastAnswer = currentAnswer;
          this.ladtLocation = location;
          this.$refs['card ' + location][0].classList.add(`pressed`);
          this.numOfTry = 1;
        }
        else if (this.numOfTry === 1) {
          this.$refs['card ' + location][0].classList.add(`pressed`);
          if (currentAnswer === this.lastAnswer && this.ladtLocation != location) {
            this.corrrectAnswer += 1;
            this.$refs['card ' + location][0].classList.add(`couple${currentAnswer}`);
            this.$refs['card ' + this.ladtLocation][0].classList.add(`couple${currentAnswer}`);
          }
          else {
            this.$refs['card ' + location][0].classList.add(`shake`);
            this.$refs['card ' + this.ladtLocation][0].classList.add(`shake`);
          }

          this.lastAnswer = 0;
          this.ladtLocation = 0;
          this.numOfTry = 0;
        }
      }
    },
    removeShake (event) {
      event.currentTarget.classList.remove('shake');
      event.currentTarget.classList.remove('pressed');
      this.$refs['card ' + this.ladtLocation][0].classList.remove(`pressed`);
    },
    nextPage() {
      this.$emit(`nextPage`, 3);
    },
    startLearn() {
      this.showContent = true;
    },
  },
  computed: {
    shuffleKeys() {
      let arr = Object.keys(this.answers);
      let tmp = arr.slice();
      for (let i = 0; i < arr.length; i++) {
        let index = Math.floor(Math.random() * tmp.length);
        arr[i] = tmp[index];
        tmp = tmp.slice(0, index).concat(tmp.slice(index + 1));
      }
      return arr;
    },
  },
}
</script>


<style scoped>
#typeBehavior {
  background-image: url("@/assets/artboard.svg");
  background-size: cover;
  width: 100vw;
  height: 100vh;
  background-repeat: no-repeat;
  position: absolute;
  overflow: hidden;
  z-index: -2;
}


.next {
  display: block;
  position: absolute;
  bottom: 30vh;
  left: 18%;
  transform: translateX(-50%);
}

.card {
  width: 10vw;
  height: 12vw;
  background-color: rgb(153, 229, 153);
  opacity: 70%;
  border-radius: 5%;
  cursor: pointer;
  position: relative;
  color: black;
  text-align: center; 
  display: flex;
  direction: rtl;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  font-size: 1.2rem;
  padding: 0 0.5rem;
}

.pressed {
  border: 3px solid white;
}

.card:hover {
  background-color: rgb(102, 182, 102);
}

.cards {
  position: relative;
  top: 15vh;
  left: 25vw;
  display: flex;
  width: 49vw;
  height: 60vh;
  flex-wrap: wrap;
  justify-content: space-between;
}


.couple1::before {
  content: "";
  width: 98%;
  height: 98%;
  border: 8px solid rgb(136 211 239);
  border-radius: 8px;
  position: absolute;
  z-index: -1;
  top: -1%;
  left: -2%;
  animation: spin 2.5s linear infinite;
}

.couple2::before {
  content: "";
  width: 98%;
  height: 98%;
  border: 8px solid rgb(193 130 193);
  border-radius: 8px;
  position: absolute;
  z-index: -1;
  top: -1%;
  left: -2%;
  animation: spin 2.5s linear infinite;
}

.couple3::before {
  content: "";
  width: 98%;
  height: 98%;
  border: 8px solid rgb(235, 235, 132);
  border-radius: 8px;
  position: absolute;
  z-index: -1;
  top: -1%;
  left: -2%;
  animation: spin 2.5s linear infinite;
}

.couple0::before {
  content: "";
  width: 98%;
  height: 98%;
  border: 8px solid pink;
  border-radius: 8px;
  position: absolute;
  z-index: -1;
  top: -1%;
  left: -2%;
  animation: spin 2.5s linear infinite;
}

.shake {
  animation: shake 1s;
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
    transform: rotate(5deg);
  }

  25% {
    transform: rotate(-5deg);
  }

  50% {
    transform: rotate(2deg);
  }

  75% {
    transform: rotate(-5deg);
  }

  100% {
    transform: rotate(-2deg);
  }
}
</style>