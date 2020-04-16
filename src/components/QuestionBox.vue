<template>
  <div class="question-box-container">
  <b-jumbotron>
  

    <template slot="lead">
      {{ currentQuestion.question }}
    </template>

    <hr class="my-4">

    <p >
     
       <b-list-group>
  <b-list-group-item v-for="(answer,index) in answers" :key="index" @click="selectedAnswer(index)" 
    :class="[ !answered && selectedIndex === index?'selected': 
          answered && correctIndex == index ? 'correct':
           answered &&selectedIndex === index && correctIndex != index ? 'incorrect':''  ]"  >{{answer}} </b-list-group-item>

</b-list-group>
    </p>

    <b-button variant="primary" @click="submiteAnswer" :disabled="selectedIndex === null || answered">Submit</b-button>
    <b-button @click="next" variant="success" href="#">Next</b-button>
  </b-jumbotron>
</div>
</template>
<script>
import _ from 'lodash';
export default {
  props:{
  currentQuestion:Object,
  next: Function,
  increment:Function
  },
  data: function (){
return {
  selectedIndex:null,
  correctIndex:null,
  answered:false,
 sheffledAnswers:[]
}
  },

watch: {
  currentQuestion:{
    immediate:true,
    handler(){
      this.selectedIndex=null,
      this.answered=false, 
      this.shuffleAnswers()
    }
  }
  
//   (){
//   this.selectedIndex=null
//   this.shuffleAnswers()
// }
},
  methods:{
    submiteAnswer(){
      let isCorrect = false;

      if(this.selectedIndex == this.correctIndex){
        isCorrect=true
      }
      this.answered=true
      this.increment(isCorrect)

    },
    selectedAnswer(index){
    this.selectedIndex = index
    },
    shuffleAnswers(){
let answers = [...this.currentQuestion.incorrect_answers,this.currentQuestion.correct_answer]
//  this.sheffelAnswers = _.shuffle(answers)

 this.sheffledAnswers=_.shuffle(answers)
  this.correctIndex = this.sheffledAnswers.indexOf(this.currentQuestion.correct_answer)


}
  },

  computed:{
    answers(){
      let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer)
    return answers
    }
  }
}
</script>

<style scoped>
.list-group{
  margin-bottom: 15px
}
.list-group-item:hover{
 background-color: #EEE;
 cursor: pointer;
}
.button{
  margin: 0 15px;
}
.selected{
background-color:lightblue

}
.correct{
  background-color:lightgreen
}
.incorrect{
    background-color:lightcoral
}
</style>