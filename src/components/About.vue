<template>
    <div id="about">
        <img class="icon" src="@/assets/aboutIcon.svg" @click="showAbout">
        <div class="all">
            <div v-show="show" class="container">
                <div class="text">
                    <img class="close" src="@/assets/closeIcon.svg" @click="closeAbout">
                    <div class="container-titles">
                        <div> ראש מדור טי"ל</div>
                        <div> רס"ם שלומי אוגרן</div>
                    </div>
                    <div class="container-titles">
                        <div>ראש תחום מו"פ וחדשנות בלמידה</div>
                        <div>רס"ל אביב ואנונו</div>
                    </div>
                    <div class="container-titles">
                        <div>מפתחת לומדה</div>
                        <div>טוראי גילי אלבז</div>
                    </div>
                    <div class="container-titles">
                        <div>מעצב UX & UI</div>
                        <div>סמל גפן קופרמן</div>
                    </div>
                    <div class="container-titles">
                        <div>מומחה תוכן</div>
                        <div>סמל גילי שוורץ</div>
                    </div>
                    <div class="container-titles">
                        <div>גרסה</div>
                        <div>08/2023</div>
                    </div>
                    <div class="container-titles">
                        <div>צור קשר:</div>
                        <a href="mailto:madortill@gmail.com">madortill@gmail.com</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "about",
    data() {
      return {
          show: false,
      }
    },
    methods: {
        showAbout() {
            this.show = true;
        },
        closeAbout() {
            this.show = false;
        }
    },
    computed: {

    }
  }
  </script>
  
  <style scoped>

  #about {
    direction: rtl;
  }

  .icon {
    width:5vw;
    height: 5vh;
    position: fixed;
    margin-top: 1vh;
    margin-left: 95vw;
  }

  .container-titles :first-child {
    font-size: 2vmax;
    font-weight: 400;
  }

  .container-titles :last-child {
    font-size: 1.5vmax;
  }

  .text{
    position: absolute;
    width: 30vw;
    height: 70vh;
    background-color: white;
    opacity: 0.9;
    border-radius: 10%;
    z-index: 5;
    text-align: center;
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: space-evenly
  }

  .container {
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    flex-direction: column;
    flex-wrap: nowrap;
    align-items: center;
  }

  .close{
    width: 3.5vw;
    height: 3.5vh;
    position: relative;
    left: -1vw;
  }

  .all {
    position: absolute;
  }
  </style>