<template>
  <div>
    <b-jumbotron>
      <template slot="lead">
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4">

      <b-list-group>
        <b-list-group-item v-for="(answer, index) in shuffledAnswers" :key="index"
          @click="selectAnswer(index)" 
          :class="answerClass(index)"  
          
        >          
          {{answer}}
        </b-list-group-item>
      </b-list-group>


      <b-button variant="primary"
      @click="submitAnswer"      
      :disabled="selectedIndex === null || submitted"
      >
        
        
        Submit</b-button>

      <b-button  variant="success" @click="next(); changeSubmit();">Next</b-button>
    </b-jumbotron>
  </div>
</template>


<script>
import _ from 'lodash'
  export default {
    props: {
      currentQuestion: Object,
      next: Function,
      increment: Function
    },

    data () {
      return {
        selectedIndex: null,
        shuffledAnswers: [],
        submitted: false,
        correctIndex: null
       
      
       
      }
    },

    computed: {
      answers() {
        let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer);
        return answers;

      }
    },

    watch: {
      currentQuestion:{
        immediate: true,
        handler(){
           this.selectedIndex = null
          this.shuffleAnswers()
        }
      },
      
    },
    methods: {
      selectAnswer(index){
        this.selectedIndex = index 
        console.log(index);
      },
      shuffleAnswers(){
        let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
        this.shuffledAnswers = _.shuffle(answers);
        this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
      },
      submitAnswer(){
        let isCorrect = false;
            if (this.selectedIndex === this.correctIndex) {
               
               isCorrect = true;
              }
              this.increment(isCorrect);
              this.submitted = true;
              console.log(isCorrect);
              

      },
      changeSubmit(){
        this.submitted = false;
      },
      answerClass(index){
        let answerClass = '';
        if ( !this.submitted&&this.selectedIndex === index) {
           answerClass = 'selected'
        } else if( this.submitted && this.  correctIndex === index){
            answerClass = 'correct'
        } else if(this.submitted && this.selectedIndex === index && this. correctIndex !== index){
          answerClass = 'incorrect'
        }
      
        return answerClass;
       
      }
    }
  }
</script>

<style scoped>
.list-group{
  margin-bottom: 15px;
}

.btn{
  margin: 5px;
}


.list-group-item:hover{
  background: #EEE;
  cursor: pointer;
}

.selected{
  background-color: lightblue;
}
.correct{
  background-color: rgb(91, 212, 91)
}
.incorrect{
  color: white;
  background-color:firebrick;
 
}
</style>
