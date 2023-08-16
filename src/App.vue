<template>
    <div id="app">
      <span v-if="numPage === 1">
        <div v-if="!start" class="black"></div>
        <div v-if="start" class="startText">
          <button @click="changePage(2)" >המשך</button>
        </div>
    </span>
    <!-- <board v-if="numPage === 2"></board> -->
    <Game @nextPage="changePage" v-if="numPage === 4"></Game>
    <typeBehavior @nextPage="changePage" v-if="numPage === 2" ></typeBehavior>
    <comments @nextPage="changePage" v-if="numPage === 3"></comments>
    <howToUse @nextPage="changePage" v-if="numPage === 5"></howToUse>
    </div>
</template>

<script>
import TypeBehavior from './components/TypeBehavior.vue'
import HowToUse from './components/HowToUse.vue'
import Comments from './components/Comments.vue'
// import Board from './components/Board.vue'
import Game from './components/Game.vue'
export default {
  components: {TypeBehavior, HowToUse, Comments, Game},
  data() {
    return {
      start: false,
      numPage: 1
    }
  },
  mounted () {
    setTimeout(() => {
      this.start = true;
    }, 2000);
  },
  methods: {
    changePage(numPage) {
      this.numPage = numPage;
      console.log(this.numPage);
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

</style>
