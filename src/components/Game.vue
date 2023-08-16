<template>
    <div id="game">
        <button @click="nextPage()">המשך</button>
    </div>
</template>

<script>
export default {
  name: "game",
  data() {
    return {
        firstOpen:[{
                question: `לאיזה שני סוגים מתייחסת התגובה "שיקוף" ?`,
                trueAnswer:"מילולי והשלכות"
            },
            {
                question: "",
                trueAnswer:""
            }
        ],
        firstClose:[
            {
                question: "מהי הפרעה ממשית?",
                answer1:" התנהגות שפוגעת בתהליך הלמידה- בחניך או סביבתו",
                answer2:" התנהגות שאינה פוגעת כלל בתהליך הלמידה",
                answer3:" התנהגות מכוונת שפוגעת בתהליך הלמידה ונובעת מסיבות אישיות של החניך"
            },
            {
                question: "נשתמש בתגובה של מבט כתגובה להפרעה",
                answer1:"קלה",
                answer2:"קשה",
                answer3:"בינונית"
            },
            {
                question: "מדריך נכנס לכיתה ושם לב שמרבית החניכים מתעסקים בנייד שלהם.לכן, החליט לרכז את כלל הניידים בקופסא ולהחזירם בסוף השיעור.באיזו תגובה פעל המדריך?",
                answer1:" שיקוף ותיאור השלכות",
                answer2:" הגדרת חוזה התנהגותי",
                answer3:" סילוק גורמים מסיחים"
            },
            {
                question: "לפני שיעור חניך משתף אותך בכך שהוא לא מרגיש שהחומר רלוונטי אליו ולכן אין סיבה שיהיה נוכח בשיעור. איזו תגובה הכי מתאימה בסיטואציה זו?",
                answer1:"קרבה פיזית",
                answer2:"שתיקה",
                answer3:"סילוק ידידותי"
            }
        ],
        secondOpen: 
            {
                question: "",
                trueAnswer:""
            },
        secondClose: [
            {
                question: "",
                trueAnswer:"",
                answer1:"",
                answer2:""
            },
            {
                question: "",
                trueAnswer:"",
                answer1:"",
                answer2:""
            },
            {
                question: "",
                trueAnswer:"",
                answer1:"",
                answer2:""
            }
        ],
        numLogin: 1,
    }
  },
  methods: {
    nextPage() {
        this.$emit(`nextPage`,5);
    }
  }
}
</script>


<style scoped>
</style>