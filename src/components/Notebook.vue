<template>
    <div id="notebook">
        <div class="notebook" :class="numText===1 ? 'finish' : ''">
            <div class="right">
                <div class="page-inner" contenteditable>
                    <div><br></div><div>&nbsp; &nbsp;{{ arr[numText] }}&nbsp;</div>
                </div>
                <button id="go" v-if="numText === 0" @click="nextPage">בואו נתחיל</button>
            </div>
        </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['numText'],
    name: "notebook",
    data() {
      return {
          arr: [`ברוכים הבאים ללומדת "התמודדות עם התנהגויות הלומדים, כפי ששמתם לב נכנסתם לכיתה חסרת ריכוז ובה כל חניך עסוק במשהו אחר, בוא נלמד איך להשיב את קשב החניכים אלינו"`, " כל הכבוד, הצלחתם לרכז את כלל התלמידים, כל שנותר לעשות זה להעביר את החומר הרצוי בצורה נכונה, בהצלחה!! "],
        //   buttonArr: ["בואו נתחיל", "בא לי שוב"]
      }
    },
    methods: {
        nextPage() {
                this.$emit(`nextPage`,2);
        },
    },
  }
  </script>
  
  <style scoped>
  /* .finish {
    background-image: url("@/assets/media/class3.png");
  background-size: cover;
  width: 100vw;
  height: 100vh;
  background-repeat: no-repeat;
  position: absolute;
  overflow: hidden;
  background-position: bottom;
  z-index: -2;
  } */
.notebook {
    direction: rtl;
  position: absolute;
  width: 40vw; height: 40vh;
  top: 40%; left: 40%;
  margin: -175px 0 0 -250px;
  background-color: #444;
  background-image:
    -webkit-repeating-radial-gradient(
      center center,
      rgba(0,0,0,.5),
      rgba(0,0,0,.5) 2px,
      transparent 2px,
      transparent 100%
    );
  background-image:
    repeating-radial-gradient(
      center center, 
      rgba(0,0,0,.5), 
      rgba(0,0,0,.5) 2px, 
      transparent 2px, 
      transparent 100%
    );
  background-size: 4px 4px;
  
  border-radius: 15px;
  box-shadow:
    inset 2px 2px 2px rgba(255,255,255,.2),
    2px 2px 3px rgba(0,0,0,.2);
}

#go {
  position: absolute;
  top: 45%;
  right: 35%;
}

.right {
  position: absolute;
  left: 50%; right: 10px;
  top: 10px; bottom: 10px;
  background: rgb(247, 246, 212);
  border-radius: 0 10px 10px 0;
  box-shadow:
    inset 10px 0 30px -10px rgba(0,0,0,.3),
    2px 2px 1px rgba(0,0,0,.8);
}

.page-inner {
  position: absolute;
  top: 30px; bottom: 20px;
  left: 15px; right: 15px;
  outline: none;
  overflow: hidden;
  background: linear-gradient(
    to bottom,
    transparent,
    transparent 19px,
    rgba(0,0,0,.2),
    rgba(0,0,0,.2) 1px
  );
  background-size: 100% 20px;
  box-shadow:
    0 -1px 0 rgba(0,0,0,0.2),
    0 -5px 0 rgb(247, 246, 212),
    0 -6px 0 rgba(0,0,0,0.4);
  
  font: 1vw/20px 'Courgette';
  color: #555;
  text-align: right;
}
.page-inner > div {text-align: center !important}
  </style>