<template>
  <div id="animationType">
    <span class="typewriter">
      <h1 :style="lineLenght">{{ arr[numText] }}</h1>
      <button :disabled="start" @click="startLearn()" > למד אותי </button>
    </span>
  </div>
</template>

<script>
export default {
  props: ['numText'],
  name: "animationType",
  data() {
    return {
        arr: ["סוגי ההתנהגות של הלומדים,נלמד באמצעות משחק הזיכרון ", "תגובות אפשריות של המדריך", "עקרונות לבחירה ושימוש בתגובה"],
        start: true
    }
  },
  mounted () {
    setTimeout(() => {
      this.start = false;
    }, 5000);
  },
  methods: {
    startLearn() {
        this.$emit("startLearn");
    }
  },
  computed: {
    lineLenght() {
      if(this.numText === 0) {
        return {
          "width" : "43vw"
        }
      }
      else if(this.numText === 1) {
        return {
          "width" : "20vw"
        }
      }
      return {
        "width" : "30vw"
      }
    },
  }
}
</script>

<style scoped>
.typewriter h1 {
  direction: rtl;
  color: black;
  font-family: monospace;
  overflow: hidden; 
  border-left: .15em solid; 
  white-space: nowrap; 
  margin: 0 auto;
  letter-spacing: .15em; 
  width: 43vw;
  animation: 
    typing 3.5s steps(30, end),
    blink-caret .5s step-end infinite;
}

.typewriter {
  position: relative;
  top: 20vh;
}

.typewriter button{
  display: block;
  margin: 0 auto;
  margin-top: 2vh;
}


@keyframes typing {
  from { width: 0 }
  to { width: lineLenght }
}


@keyframes blink-caret {
  from, to { border-color: transparent }
  50% { border-color: black }
}
</style>