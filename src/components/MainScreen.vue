<template>
    <div id="mainScreen">
        <span class="pupils">
            <div @click="goQuestion()" :key="i.index" v-for="(i) in arr" class="pupil"></div>
        </span>
        <Game v-if="question"></Game>
    </div>
</template>

<script>
import Game from './Game.vue'
export default {
  components: {Game},
  props: ['numLogin'],
  name: "mainScreen",
  data() {
    return {
        start: false,
        arr: [0,1,2,3,4,5,6,7,8,9],
        question: false,
    }
  },
  mounted () {
    setTimeout(() => {
      this.start = true;
    }, 2000);
  },
  methods: {
    changePage() {
      this.numLogin++;
      // console.log(this.numLogin);
      this.$emit(`nextPage`,2);
    },
    goQuestion() {
      this.question = true;
    }
  }
}
</script>


<style scoped>
.black{
  width: 100vw;
  height: 100vh;
  background-color: black;
  animation: openscreen 2s  forwards;
}

@keyframes openscreen {
    from {
      opacity: 70%;
    }
    to {
      opacity: 0%;
    }
}

.startText{
  margin-top: 25vh;
  width: 40vw;
  height: 20vw;
  background-color: black;
  margin-bottom: -88vh;
  margin-left: 25vw;
  border-radius: 5%;
}

button{
  background-color: black;
  color: white;
  border-color: white;
  border-radius: 5%;
  margin-top: 45%;
  margin-left: 45%;
}

.pupil{
    width: 10vw;
    height: 15vw;
    background-color: black;
    border-radius: 5%;
    cursor: pointer;
    padding: 3px;
    position: relative;
    margin-left: 5vw;
}

.pupils{
    position: absolute;
    top: 25vh;
    left: 6vw;
    display: flex;
    width: 80vw;
    height: 70vh;
    flex-wrap: wrap;
    justify-content: space-between;
    z-index: -1;
}

</style>