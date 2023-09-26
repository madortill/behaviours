<template>
    <div id="app">
      <navbar  v-if="numPage > 1 && numPage !== 4 " id="navbar" @goToPage="changePage" :navbarArr="navbarArr"></navbar>
      <span v-if="numPage === 1">
        <div v-if="!start" class="black"></div>
        <notebook @nextPage="changePage" v-if="start" :numText="0"></notebook>
      </span>
    <Game @saveArr="saveArr" :successes="gameArr" :numLogin="numLogin" @nextPage="changePage" v-if="numPage === 4"></Game>
    <typeBehavior @nextPage="changePage" v-if="numPage === 2" ></typeBehavior>
    <comments @nextPage="changePage" v-if="numPage === 3"></comments>
    <howToUse @nextPage="changePage" v-if="numPage === 5"></howToUse>
    </div>
    <notebook @nextPage="changePage" v-if="numPage === 6" :numText="1"></notebook>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Notebook from './components/Notebook.vue'
import TypeBehavior from './components/TypeBehavior.vue'
import HowToUse from './components/HowToUse.vue'
import Comments from './components/Comments.vue'
import Game from './components/Game.vue'
export default {
  components: {TypeBehavior, HowToUse, Comments, Game, Notebook, Navbar},
  data() {
    return {
      start: false,
      numPage: 3,
      numLogin: 1,
      gameArr: [],
      navbarArr: [true, true, false, false, true, false]
    }
  },
  mounted () {
    setTimeout(() => {
      this.start = true;
    }, 2000);
  },
  methods: {
    changePage(numPage) {
      this.navbarArr[numPage] = true
      if(numPage === 1) {
        this.start = true;
        this.numPage = 1;
        this.numLogin = 1;
        this.gameArr = [];
      }
      if (numPage === 4 && this.numPage === 5){
        this.numLogin = 2;
      }
      this.numPage = numPage;
    },
    saveArr(arrGame) {
      this.gameArr = arrGame;
    }
  }
}
</script>


<style scoped>
#navbar{
  position: relative;
  z-index: 3;
}
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
