<template>
  <div class="container-app">
    <div class="container-quiz">
      <div class="quiz-header">
        <h1>Quiz App</h1>
      </div>
      <div class="step-progress" :style="{'width':progress+'%'}"></div>
      <div class="main-quiz"  v-for="(element,index) in questions.slice(a,b)" :key="index" v-show="quiz">
        <div class="box-question">
          <h2>Question {{b}}/{{questions.length}}</h2>
          <p>{{element.question}}</p>
        </div>
        <div class="box-suggerstions">
          <ul>
            <li v-for="(item,index) in element.suggestions" :key="index" :class="select? check(item) :''" @click=" seletResponse(item)">
              {{item.suggestion}}
              <div class="fas fa-check" v-if="select?item.correct:''"></div>
              <div class="fas fa-times" v-if="select?!item.correct:''"></div>
            </li>
          </ul>
        </div>
      </div>
      <div class="box-score" v-if="score_show || last">
        <h2>Yout score is</h2>
        <h2>{{ score}}/{{questions.length}}</h2>
        <div class="btn-restart">
          <button @click="restartQuiz">Restart <i class="fas fa-sync-alt"></i></button>
        </div>
      </div>
      <div class="quiz-footer">
        <div class="box-button" v-if="quiz">
          <button @click=" SkipQuestion" :style="!next?'background-color:rgba(10,120,202)':''">Skip</button>
          <button @click="nextQuestion" :style="next?'background-color:rgba(10,128,202)':''">Next</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      questions: [
        {
          question:'inside with Html element do we put the javascript?',
          suggestions:[
            {suggestion:'<script>',correct:true},
            {suggestion:'<js>'},
            {suggestion:'<scripts>'},
            {suggestion:'<scripttt>'},
          ]
        },//qus
        {
          question:'inside with Html element do we put the javascript?',
          suggestions:[
            {suggestion:'<js>'},
            {suggestion:'<scripts>'},
            {suggestion:'<script>',correct:true},
          ]
        },//qus
        {
          question:'inside with Html element do we put the javascript?',
          suggestions:[
            {suggestion:'<script>',correct:true},
            {suggestion:'<js>'},
            {suggestion:'<scripts>'},
            {suggestion:'<scripttt>'},
          ]
        },//qus
        {
          question:'inside with Html element do we put the javascript?',
          suggestions:[
                        {suggestion:'<scripts>'},
            {suggestion:'<scripttt>'},
            {suggestion:'<script>',correct:true},
            {suggestion:'<js>'},
          ]
        },//qus
        {
          question:'inside with Html element do we put the javascript?',
          suggestions:[
            {suggestion:'<js>'},
            {suggestion:'<script>',correct:true},
            {suggestion:'<scripts>'},
            {suggestion:'<scripttt>'},
          ]
        },//qus
      ],
      a:0,
      b:1,
      select:false,
      score:0,
      score_show:false,
      quiz:true,
      next:false,
      progress:0,
      last:false
    }
  },
  methods:{
    seletResponse(item){
      this.lastCheck();

       if(!this.select){
         this.select=true;
          if(item.correct && this.select){
        this.score++;
          console.log(this.score)
      }
       }
      this.next=true;

     

         if(this.last){
        this.nextQuestion();
        return
      }
    },
    check(status){
      if(status.correct){
        return 'correct'
      }else{
        return 'incorrect'
      }
    },
    nextQuestion(){
        if(!this.next){
          alert("문제를 풀어주세요")
        return
      }
      this.progress=this.progress+(100/this.questions.length)
      if(this.questions.length-1 === this.a){
        this.score_show=true;
        this.quiz=false
      }else{
          this.a++;
          this.b++;
          //초기화
          this.select=false;
          this.next=false
      }
   
    },
    SkipQuestion(){
      if(this.next){
         console.log(this.next)
        return
      }
     this.progress=this.progress+(100/this.questions.length)
       if(this.questions.length-1 === this.a){
        this.score_show=true;
        this.quiz=false
      }else{
          this.a++;
          this.b++;
      // this.select=false;
      }
    },
    restartQuiz(){
    this.progress=this.progress+(100/this.questions.length)
      Object.assign(this.$data,this.$options.data()) //리셋
    },
    lastCheck(){
      (this.a === this.questions.length-1)?this.last=true:this.last=false
      console.log('라스트',this.last)
    }
  }
}
</script>


