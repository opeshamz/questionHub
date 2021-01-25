<template>
  <div class="b-icon">
    <b-jumbotron class="questions" >

      <template #lead>
        {{ currentQuestion.question}}
      </template>

      <hr class="my-4">

      <b-list-group>
        <b-list-group-item
            v-for="(answers, index) in answers" :key="index"
            @click="selectAnswers(index)"
          :class="[selectedIndex === index ? 'selected':'']"
        >{{answers}}
        </b-list-group-item>
      </b-list-group>
      <b-row class="mt-4 justify-content-md-center" md="auto" align-h="around" >
        <b-button variant="outline-primary" class="w-25 btn" pill>submit</b-button>
        <b-button variant="outline-success" class="w-25 btn"  @click="next" pill>next</b-button>
        <b-button variant="outline-success" class="w-25 btn" @click="previous" pill>previous</b-button>
      </b-row>

    </b-jumbotron>
  </div>


</template>

<script>
import _ from 'lodash';
export default {

  props:{
        currentQuestion: Object,
        next:Function,
        previous: Function

},
data(){
return{
  selectedIndex: null,
  shuffleAnswer:[]
}
},
computed:{
    answers(){
    let answers = [...this.currentQuestion.incorrect_answers]
    answers.push(this.currentQuestion.correct_answer)
    return answers
    }
},
watch:{
  currentQuestion(){
      this.selectedIndex=null
this.shuffleAnswer()
  }
},
methods:{
selectAnswers(index){
  this.selectedIndex= index
},

},
  shuffleAnswer () {
let answers =[...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
this.shuffleAnswer = _.shuffle(answers)
  },

}
</script>

<style scoped>
.questions{
background-color: #ECDA9A;
}
.btn{
 margin: auto;
}
.list-group-item:hover{
  background: #84784D;
  cursor: pointer;

}

.selected{
  background-color: #ACA486;
}
.corectAnswers{
  background-color: #9BBB27;
}
.wrongAnswers{
  background-color: red;
}
</style>
