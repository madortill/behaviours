<template>
    <div id="game">
        <span v-if="showInstruction">
            <div class="instruction">
                <p class="textInstruction">עם הידע שצברתם, אתם יודעים איך לרכז את התלמידים בכיתה. תוכלו לעשות זאת בלחיצה על כל תלמיד שתרצו לעזור לו, בלחיצה על התלמיד תפתח שאלה שבמידה ותענו עליה נכון הריכוז של התלמידה ייהיה כל כולו שלכם, לכל שאלה פתוחה יהיו לכם שלוש ניסיונות. בהצלחה!</p>
            </div>
            <button @click="gameOrInstruction">למשחק</button>
        </span>
        <img  src="@/assets/instructionIcon.png" v-if="!showInstruction" @click="gameOrInstruction" class="toInstruction">
        <span class="pupils">
            <span class="row3" :style="numberTrueAnswer > 6 ? '' : 'filter: grayscale(0.7);'" :class="numberTrueAnswer > 6 ? '' : 'rowDone'">
                <img @click="goQuestion(index+7)" :key="index" v-for="(value, index) in imgRow3" :src="value" :id="'student' + index"  class="pupil" />
            </span>
            <span class=" row2" :style="numberTrueAnswer < 4 ? 'filter: grayscale(0.7);' : ''" :class="(numberTrueAnswer > 6)|| (numberTrueAnswer < 3)  ? ' rowDone' : ''">
                <img  @click="goQuestion(index+4)" :key="index" v-for="(value, index) in imgRow2" :src="value" :id="'student' + index"  class="pupil" />
            </span>
            <span class="row1" :class="numberTrueAnswer > 3 ? ' rowDone' : ''">
                <img  @click="goQuestion(index)" :key="index" v-for="(value, index) in imgRow1" :src="value" :id="'student' + index"  class="pupil" />
            </span>
        </span>
        <div class="question" v-if="showQuestion && arr[numOuestion] === 1">
            <ul> {{close1[numOuestionClose].question}}
                <li @click="checkAnswer(1)">{{close1[numOuestionClose].answer1}}</li>
                <li @click="checkAnswer(2)">{{close1[numOuestionClose].answer2}}</li>
                <li @click="checkAnswer(3)">{{close1[numOuestionClose].answer3}}</li>
            </ul>
            <p v-show="isTrueAnswer">כל הכבוד, תשובה נכונה</p>
            <p v-show="!isTrueAnswer && numTry > 0">נסה שוב</p>
        </div>
        <div class="question" v-if="showQuestion && arr[numOuestion] === 2">
            <p>{{open1[numOuestionOpen].question}}</p>
            <input v-if="showQuestion" type="" v-model="answer">
            <button  @click="checkAnswer(4)">בדוק אותי</button>
            <p v-show="isTrueAnswer">כל הכבוד, תשובה נכונה</p>
            <p v-show="!isTrueAnswer && numTry === 1">נסה שוב</p>
            <p v-show="!isTrueAnswer && numTry === 2">התשובה הנכונה היא: {{open1[numOuestionOpen].trueAnswer}}</p>
        </div>
    </div>
</template>

<script>
export default {
  name: "game",
  props:["numLogin","successes"],
  data() {
    return {
        open1:[{
                question: `לאיזה שני סוגים מתייחסת התגובה "שיקוף" ?`,
                trueAnswer:"מילולי והשלכות"
            },
            {
                question: `במהלך שיעור העיר מדריך לחניכים: "אתם לא מפסיקים לדבר בניכם מתחילת השיעור". באיזה תגובה השתמש במדריך ?`,
                trueAnswer:"שיקוף מילולי"
            },
            {
                question: " במהלך שיעור מדריך העיר מספר פעמים לחניך עד שהחליט להוציא אותו מהכיתה.  החניך התווכח, ביקש הזדמנות נוספת והבטיח שלא יפריע יותר למהלך השיעור .המדריך השתכנע ובחר להשאיר אותו בכיתה, על איזה עקרון לא שמר המשריך?",
                trueAnswer:"החלטיות"
            },
            {
                question: "במהלך שיעור שני תלמידים שיחקו בטלפון. כאשר ליאור שיחק המדריך ביקש ממנו להפסיק לשחק אך כאשר רועי שיחק, המדריך הוציא אותו מהכיתה. איזה עקרון לא התממש בבחירת התגובה של המדריך?",
                trueAnswer:"אחידות ועקביות",
            }
        ],
        close1:[
            {
                question: "מהי הפרעה ממשית?",
                answer1:" התנהגות שפוגעת בתהליך הלמידה- בחניך או סביבתו",
                answer2:" התנהגות שאינה פוגעת כלל בתהליך הלמידה",
                answer3:" התנהגות מכוונת שפוגעת בתהליך הלמידה ונובעת מסיבות אישיות של החניך"
            },
            {
                question: "נשתמש בתגובה של מבט כתגובה להפרעה",
                answer1:"בינונית",
                answer2:"קשה",
                answer3:"קלה"
            },
            {
                question: "מדריך נכנס לכיתה ושם לב שמרבית החניכים מתעסקים בנייד שלהם.לכן, החליט לרכז את כלל הניידים בקופסא ולהחזירם בסוף השיעור.באיזו תגובה פעל המדריך?",
                answer1:" שיקוף ותיאור השלכות",
                answer2:" הגדרת חוזה התנהגותי",
                answer3:" סילוק גורמים מסיחים"
            },
            {
                question: "לפני שיעור חניך משתף אותך בכך שהוא לא מרגיש שהחומר רלוונטי אליו ולכן אין סיבה שיהיה נוכח בשיעור. איזו תגובה הכי מתאימה בסיטואציה זו?",
                answer1:"שתיקה ",
                answer2:"קרבה פיזית",
                answer3:"סילוק ידידותי"
            },
            {
                question: "על איזה עקרון עלייך לשמור כדי למנוע איבוד אפקטיביות של תגובה ופיתוח חסינות אליה אצל חניכים?",
                answer1:"התאמה",
                answer2:"הדרגתיות",
                answer3:"גיוון"
            },
            {
                question: "חניך התנהג בצורה מופתית לאורך כל השיעור אך לפתע התנהג באלימות כלפי חניך אחר. על איזה עקרון נוותר במקרה זה?",
                answer1:"רגישות",
                answer2:"הדרגתיות",
                answer3:"החלטיות" 
            }
        ],
        imgRow3: ["/music.png","/sleep.png","/phone.png"],
        imgRow2: ["/book2.png","/phone.png","/nail.png",],
        imgRow1:["/shout.png","/talk.png","/book.png","/music2.png"],
        imgGoodStud:["/darkBrownGoodStude.png","/blondGoodStude.png","/blackGoodStude.png","/darkBrownGoodStude.png","/blackGoodStude.png","/brownGoodStude.png","/redGoodStude.png","/darkBrownGoodStude.png","/blondGoodStude.png","/brownGoodStude.png"],
        answer: "",
        arr: [1,1,2,1,2,1,1,2,1,2],
        showQuestion: false,
        numOuestion: 0 ,
        numOuestionOpen: 0,
        numOuestionClose: 0,
        trueAnswer: [1,3,1,2,3,2],
        numberTrueAnswer: 0,
        showInstruction: true,
        isTrueAnswer: false,
        numTry: 0,
        arrSuccesses:[],
        numberAnswer: 0
    }
  },
  mounted () {
    if (this.numLogin === 2){
        this.numOuestionOpen +=2;
        this.numOuestionClose +=4;
        this.numberTrueAnswer +=6;
        this.arrSuccesses = this.successes;
        this.imgRow1 = ["/darkBrownGoodStude.png","/blondGoodStude.png","/blackGoodStude.png","/darkBrownGoodStude.png"];
        this.imgRow2 = ["/blackGoodStude.png","/brownGoodStude.png","/nail.png",];
    }
  },

  methods: {
    gameOrInstruction() {
        this.showInstruction = !this.showInstruction;
    },

    goQuestion(x) {
        console.log(x);
        if ((this.numLogin === 1 && x < 6) || (this.numLogin === 2 && x > 5)){
            this.numberAnswer = x;
            let xInArr = false;
            for (let i = 0; i < this.arrSuccesses.length; i++) { 
                if (this.arrSuccesses[i] === x){
                    xInArr = true;
                }
            }
            if(this.showQuestion === false && !xInArr){
                this.numOuestion +=1;
                this.showQuestion = true;
            }
        }
    },

    // goQuestion(x) {
    //     if ((this.numLogin === 1 && x < 6) || (this.numLogin === 2 && x > 5)){
    //         this.numberAnswer = x;
    //         if(this.showQuestion === false){
    //             this.numOuestion +=1;
    //             this.showQuestion = true;
    //         }
    //     }
    // },

    checkAnswer(number) {
        if(number===4){
            if(this.answer === this.open1[this.numOuestionOpen].trueAnswer) {
                this.isTrueAnswer = true;
                setTimeout(() => {
                    this.arrSuccesses[this.numberTrueAnswer] = this.numberAnswer;
                    this.isTrueAnswer = false;
                    this.showQuestion = false;
                    this.numberTrueAnswer++;
                    this.numOuestionOpen +=1;
                    this.answer = "";
                    this.numTry = 0;
                    // console.log("gili");
                }, 1500);
                if(this.numberAnswer < 4) {
                    this.imgRow1[this.numberAnswer] = this.imgGoodStud[this.numberAnswer]
                }
                else if(this.numberAnswer < 7) {
                    this.imgRow2[this.numberAnswer-4] = this.imgGoodStud[this.numberAnswer]
                }
                else {
                    this.imgRow3[this.numberAnswer-7] = this.imgGoodStud[this.numberAnswer]
                }
            }
            else {
                if(this.numTry === 0) {
                    this.numTry++;
                    this.answer = "";
                }
                else {
                    this.numTry++;
                setTimeout(() => {
                    this.isTrueAnswer = false;
                    this.showQuestion = false;
                    this.numberTrueAnswer++;
                    this.numOuestionOpen +=1;
                    this.answer = "";
                    this.numTry = 0;
                }, 1500);
                }
            }
        }
        else if(number === this.trueAnswer[this.numOuestionClose]) {
            this.isTrueAnswer = true;
            setTimeout(() => {
                this.arrSuccesses[this.numberTrueAnswer] = this.numberAnswer;
                this.isTrueAnswer = false;
                this.showQuestion = false;
                this.numberTrueAnswer++;
                this.numOuestionClose +=1;
                this.numTry = 0;
            }, 1500);
            if(this.numberAnswer < 4) {
                    this.imgRow1[this.numberAnswer] = this.imgGoodStud[this.numberAnswer]
                }
                else if(this.numberAnswer < 7) {
                    this.imgRow2[this.numberAnswer-4] = this.imgGoodStud[this.numberAnswer]
                }
                else {
                    this.imgRow3[this.numberAnswer-7] = this.imgGoodStud[this.numberAnswer]
                }
        }
        else {
            this.numTry++;
        }
        if (this.numberTrueAnswer === 5){
            this.$emit(`nextPage`,5);
            this.$emit(`saveArr`,this.arrSuccesses)
        }
        else if(this.numberTrueAnswer === 9) {
            this.$emit(`nextPage`,6);
        }
    }
  }
}
</script>


<style scoped>
.rowDone {
    pointer-events: none;
}

#game {
    background-image: url("@/assets/media/class2.png");
  background-size: cover;
  width: 100vw;
  height: 100vh;
  background-repeat: no-repeat;
  position: absolute;
  overflow: hidden;
  background-position: bottom;
  z-index: -2;
}

button {
 margin-left: 45vw;
 margin-top: 20vh;

}
.textInstruction {
width: 40vw;
position: absolute;
text-align: center;
direction: rtl;
margin-left: 25vw;
margin-top: 20vh;
font-size: 3vh;
}
.toInstruction{
    width: 3vw;
    height: 5vh;
    margin-top: 2vh;
    margin-left: 1.5vw;
}
.instruction {
    width: 100vw;
    height: 100vh;
    background-color: white;
    opacity: 90%;
    z-index: -1;
}
.question {
    margin-top: 25vh;
    width: 40vw;
    height: 20vw;
    background-color: black;
    margin-bottom: -88vh;
    margin-left: 25vw;
    border-radius: 5%;
    color: white;
    text-align: center; 
    direction: rtl;
    font-size: 1.5vh;
}

li {
    border-radius: 10%;
    border-width: 1vh;
    border-color: aliceblue;
    width: 35%;
    margin-top: 5%;
}

.pupil {
    width: 30vw;
    height: 30vw;
    cursor: pointer;
}

.row1 {
 position: absolute;
 display: flex;
 bottom: -90vh;
 width: 90vw;
}

.row2 {
position: absolute;
 display: flex;
 bottom: -80vh;
 width: 70vw;
}

.row3 {
position: absolute;
 display: flex;
 width: 50vw;
 bottom: -70vh;
}

.pupils {
    position: absolute;
    display: flex;
    width: 100vw;
    height: 10vh;
    flex-wrap: wrap;
    justify-content: center;
    z-index: -1;
}

button {
    position: absolute;
    top: 25vh;
}
</style>