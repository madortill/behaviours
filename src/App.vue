<template>
    <div :id="numPage===1 ? 'app' : 'done'">
      <img class="logo" src="@/assets/logoTill.svg">
      <about></about>
      <navbar  v-if="numPage > 1 && numPage !== 4 && numPage !== 6" id="navbar" @goToPage="changePage" :navbarArr="navbarArr"></navbar>
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
import About from './components/About.vue'
import Navbar from './components/Navbar.vue'
import Notebook from './components/Notebook.vue'
import TypeBehavior from './components/TypeBehavior.vue'
import HowToUse from './components/HowToUse.vue'
import Comments from './components/Comments.vue'
import Game from './components/Game.vue'
export default {
  components: {TypeBehavior, HowToUse, Comments, Game, Notebook, Navbar, About},
  data() {
    return {
      start: false,
      numPage: 1,
      numLogin: 1,
      gameArr: [],
      navbarArr: [true, true, false, false, true, false],
      imgRow3: ["./music.png","./sleep.png","./phone.png"],
      imgRow2: ["./book2.png","./phone.png","./nail.png",],
      imgRow1:["./shout.png","./talk.png","./book.png","./music2.png"],
    }
  },
  mounted () {
    setTimeout(() => {
      this.start = true;
    }, 4500);
  },
  methods: {
    changePage(numPage) {
      this.navbarArr[numPage] = true
      if(numPage === 1) {
        this.start = true;
        this.numPage = 2;
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
#app {
  background-image: url("@/assets/media/class1.png");
  background-size: cover;
  width: 100vw;
  height: 100vh;
  background-repeat: no-repeat;
  position: absolute;
  overflow: hidden;
  background-position: bottom;
  z-index: -2;
}

#done {
  background-image: url("@/assets/media/class3.png");
  background-size: cover;
  width: 100vw;
  height: 100vh;
  background-repeat: no-repeat;
  position: absolute;
  overflow: hidden;
  background-position: bottom;
  z-index: -2;
}

#navbar{
  position: relative;
  z-index: 3;
}
.black{
  width: 100vw;
  height: 100vh;
  background-color: black;
  animation: openscreen 3.5s  forwards;
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

.logo {
  width:5vw;
  height: 6vh;
  position: fixed;
  margin-top: 1vh;
  margin-left: 1vh;
}


</style>
