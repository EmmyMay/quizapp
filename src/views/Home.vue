<template>
  <div class="home">
   <HeaderComp 
   :numCorrect="numCorrect"
   :numTotal="numTotal"
   
   ></HeaderComp>
   <b-container class="bv-example-row">
  <b-row>
    <b-col><QuestionBox  v-if="questions.length"
      :currentQuestion = "questions[index]"
      :next="next"
      :increment="increment"
      /></b-col>

  </b-row>
</b-container>
    
  </div>  
</template>

<script>
// @ is an alias to /src
import HeaderComp from "@/components/HeaderComp.vue";
import QuestionBox from "@/components/QuestionBox.vue";

export default {
  name: "home",
  components: {
    QuestionBox,
    HeaderComp
  },
  data () {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      disableNext: false
      
    }
    
  },
  methods: {
    next() {
      if( this.index <= 10 ){
           this.index++
      }
     
       
        this.submitted = false;
    },
    increment(isCorrect){
      if (isCorrect) {
        this.numCorrect++
      }
      this.numTotal++
      console.log(this.numCorrect);
      console.log(this.numTotal);
    }
  },
  mounted () {
    fetch(`https://opentdb.com/api.php?amount=10&category=11&difficulty=medium&type=multiple`,
      {
        method: 'get'
      }
    ) .then((res)=>{
      return res.json();
    }).then((jsonData => {
      this.questions = jsonData.results
    }))
  }
};
</script>
