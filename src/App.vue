<template>
  <div id="app">
    <Header/>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset-sm="3" >
          <QuestionBox v-if="questions.length"
          :currentQuestion="questions[index]"
          :next="next"
          :previous="previous"


          />
         </b-col >

      </b-row>
    </b-container>

  </div>
</template>

<script>
import Header from './components/Header.vue';
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
  data(){
    return{
      questions:[],
      index:0
    }
  },

methods:{
next(){
return this.index++
},
  previous(){
    return this.index--
  }
},
  mounted () {
      fetch('https://opentdb.com/api.php?amount=20&category=18&difficulty=medium',{
        method:'get'
      })
    .then((response) =>{
      return response.json()
    })
    .then((jsonData)=>{
      this.questions=jsonData.results
    })
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
