<template>
    <div class="question-box-container">
        <h1>question<span id="box" >B</span>O<span id="box">X</span></h1>
  <b-nav tabs>
    <b-nav-item disabled>Quiz App<br></b-nav-item>
    <b-nav-item disabled>Counter: {{numCorrect}} / {{numTotal}} </b-nav-item>
  </b-nav>
    </div>
</template>

<script>
export default {

  props:[
    'numCorrect',
    'numTotal'

  ],
  data () {
    return {
      
    }
  },

  methods: {
    
  }
}
</script>


<style scoped>
#box{
  color: darkkhaki
}
</style>

