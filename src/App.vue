<template>
 <div class="ctr">
     <transition name="fade" mode="out-in">
  <Question v-if="questionsAnswered < questions.length" :questions="questions" :questionsAnswered="questionsAnswered" @question-answered="questionAnswered" />
  <Result v-else :results="results" :totalCorrect="totalCorrect" />
   </transition><button type="button" @click.prevent="reset" v-if="questionsAnswered === questions.length"  class="reset-btn">Reset</button>
</div>
</template>

<script>
import Question from './components/question.vue'
import Result from './components/result.vue'
export default {
  name: 'App',
  components: {
    Question,Result
  },
  data(){
    return{
      questionsAnswered:0,
      totalCorrect:0,
      questions: [
        {
            q: 'What is 2 + 2?', 
            answers: [
                {
                    text: '4',
                    is_correct: true
                },
                {
                    text: '3',
                    is_correct: false 
                },
                {
                    text: 'Fish',
                    is_correct: false 
                },
                {
                    text: '5',
                    is_correct: false 
                }
            ] 
        },
        { 
            q: 'How many letters are in the word "Banana"?', 
            answers: [
                {
                    text: '5',
                    is_correct: false
                },
                {
                    text: '7',
                    is_correct: false 
                },
                {
                    text: '6',
                    is_correct: true 
                },
                {
                    text: '12',
                    is_correct: false 
                }
            ] 
        },
        { 
            q: 'Find the missing letter: C_ke', 
            answers: [
                {
                    text: 'e',
                    is_correct: false
                },
                {
                    text: 'a',
                    is_correct: true 
                },
                {
                    text: 'i',
                    is_correct: false 
                }
            ] 
        },
    ],
    results: [
        {
            min: 0,
            max: 2,
            title: "Try again!",
            desc: "Do a little more studying and you may succeed!"
        },
        {
            min: 3,
            max: 3,
            title: "Wow, you're a genius!",
            desc: "Studying has definitely paid off for you!"
        }
    ]
    }
  },
   methods:{
      questionAnswered(is_correct){
         if(is_correct){
           this.totalCorrect++;
         }
         this.questionsAnswered++;
      },
      reset(){
          this.questionsAnswered = 0;
          this.totalCorrect = 0;
      }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


</style>
