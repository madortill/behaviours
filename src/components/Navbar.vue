<template>
    <div id="navbar">
      <span>
      <div  @click="goToPage(2)"  id='paper1' :class="!navbarArr[2] ? 'disabled' : ''">
        <p>סוגי התנהגויות</p>
      </div>
      <div  @click="goToPage(3)" id='paper2' :class="!navbarArr[3] ? 'disabled' : ''">
        <p>תגובות המדריך ודרכי התמודדות</p>
      </div>
      <div  @click="goToPage(5)"  id='paper3' :class="!navbarArr[5] ? 'disabled' : ''">
        <p>עקרונות לבחירה ושימוש</p>
      </div>
      
    </span>
     <!-- <img @click="goToPage(2)" :disabled="true" src="@/assets/paper1.svg" :style="background">
     <p>סוגי התנהגויות</p>
     <img @click=" numPage>= 3 ? goToPage(3) : disabled" src="@/assets/paper2.svg" >
     <p>תגובות המדריך ודרכי התמודדות</p>
     <img @click="goToPage(5)" :disabled=" numPage>= 5 ? '' : disabled" src="@/assets/paper3.svg" >
     <p>עקרונות לבחירה ושימוש</p> -->
    </div>
  </template>
  
  <script>
  export default {
    props: ['navbarArr'],
    name: "navbar",
    data() {
      return {
      }
    },
    methods: {
      goToPage(numPage) {
        if(this.navbarArr[numPage]) {
          this.$emit(`goToPage`, numPage);
        }
      }
    },
    // computed: {
    //   background() {
    //     "background-image" : "url(`@/assets/paper&{}.svg`)"
    //   }
    // }
  }
  </script>
  
  <style scoped>
  #paper1{
    background-image: url("@/assets/paper1.svg");
    background-size: 100%, 100%;
    background-repeat: no-repeat;
    width: 10vw;
    height: 15vh;
    top: 0vh;
    display: inline-flex ;
    flex-direction: column;
    justify-content: center;
    position: absolute;
    left: 20vw;
  }

  #paper2{
    background-image: url("@/assets/paper4.svg");
    background-size: 100%, 100%;
    background-repeat: no-repeat;
    width: 10vw;
    height: 15vh;
    top: 0vh;
    display: inline-flex ;
    flex-direction: column;
    justify-content: center;
    position: absolute;
    left: 45vw;
  }

  #paper3{
    background-image: url("@/assets/paper3.svg");
    background-size: 100%, 100%;
    background-repeat: no-repeat;
    width: 10vw;
    height: 15vh;
    top: 0vh;
    display: inline-flex ;
    flex-direction: column;
    justify-content: center;
    position: absolute;
    left: 70vw;
  }
  
  span {
    display: flex;
    justify-content: space-around;
  }

  p {
    width: 5vh;
    text-align: center;
    margin-left: 35%;
    margin-top: 25%;
    font: 'Courgette';
  }

  .disabled {
    filter: grayscale(1);
  }
  </style>