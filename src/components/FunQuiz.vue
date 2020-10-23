<template>
    <section class="page-section bg-primary text-white mb-0">
        <div class="container">

            <!-- FunQuiz Section Heading-->
            <h2 class="page-section-heading text-center text-uppercase text-white mb-0">{{quiz.title}}</h2>
            <!-- Icon Divider-->
            <div class="divider-custom divider-light">
                <div class="divider-custom-line "></div>
                <div class="divider-custom-icon "><i class=" fas fa-star"></i></div>
                <div class="divider-custom-line "></div>
            </div>

            <div>

                <div class="jumbotron bg-light" >

                    <div class="row mt-3" v-show="startQuiz || score > 0">
                        <div class="col-md-12" >
                            <p class="text-primary" v-if="score >= 55 && questionIndex === quiz.questions.length">
                                Looks like we should grab a cup of coffee! <br> Just call me. My treat!<br>
                                 <i class="fa fa-smile fa-5x text-primary mt-2"></i>
                                
                            </p>
                            <p class="text-danger" v-if="score < 55 && questionIndex === quiz.questions.length">
                                Looks like we're not really a match eh..?<br>
                                But you may still contact me, maybe we could work something out?<br>
                                <i class="fa fa-frown fa-5x text-danger mt-2"></i>
                            </p>
                        </div>

                        
                    </div>

                    <button v-show="!startQuiz" class="btn btn-lg btn-primary" v-on:click="start">Start quiz</button>

                    <div class="" v-for="(question, index) in quiz.questions" :key="index">
                        <div class="row" v-show="index === questionIndex && startQuiz"> 
                            <div class="col-md-12 mb-5">
                                <div >
                                    <h3 class="text-primary mb-2" >{{question.text}}</h3>
                                </div>
                            </div>
                            <div class="mb-5" v-for="response in question.responses" :key="response" v-bind:class="{ 'col-md-6': question.responses.length <= 2, 'col-md-4': question.responses.length >= 3 }" >
                                <button v-bind:disabled="clicked" v-bind:value="response.correct" v-bind:name="index" class="col-md-12 btn btn-lg" v-bind:class="{ [btnDanger] : !response.correct && clicked, [btnSucess] : response.correct  && clicked, [btnOutline] : !clicked}" v-on:click="checkAnswer(response.correct)">
                                    {{response.text}}   <i v-bind:class="compClasses" ></i>
                                </button>
                            </div>
                            <div class="col-md-12 mb-2">
                                <button class="btn btn-primary" v-bind:disabled="!clicked" v-on:click="next">
                                    next question
                                </button>
                            </div>
                        </div>
                    </div>

                </div>
            </div>

        </div>
    </section>
</template>

<script>

var quiz = {
  title: 'Work with me',
  questions: [
    {
      text: "Are you looking for a developer?",
      responses: [
        {text: 'Hell yeah', correct: true}, 
        {text: 'Not sure', correct: true}, 
        {text: 'Nope', correct: false}, 
      ]
    }, {
      text: "Do you need help with a webproject?",
      responses: [
        {text: 'Hell yeah', correct: true}, 
        {text: 'Maybe', correct: true}, 
        {text: 'Nope', correct: false}, 
      ]
    }, 
    {
      text: "How many years experience should your candidate have at least?",
      responses: [
        {text: '1 year', correct: true}, 
        {text: '1 - 3 years', correct: true}, 
        {text: '+3 years', correct: false}, 
      ]
    },
    {
      text: "Do you prefer to work with mentally strong people",
      responses: [
        {text: 'Hell yeah', correct: true}, 
        {text: 'Maybe', correct: true}, 
        {text: 'Nope', correct: false}, 
      ]
    }, {
      text: "What do you think of working 9 to 5?",
      responses: [
        {text: 'Exactly how i like it', correct: false}, 
        {text: 'Thats old fashion', correct: true}, 
        {text: 'Not enaugh hours', correct: true}, 
      ]
    }, 
  

  ]
};


export default {

    data: () => ({
       quiz: quiz,
       questionIndex: 0,
       startQuiz: false,
       btnDanger: 'btn-danger',
       btnSucess: 'btn-success',
       btnOutline: 'btn-outline-primary',
       clicked: false,
       totalQuestions: 0,
       totalCorrectAnswers: 0,
       totalWrongAnswers: 0,
       score: 0
    }),
    methods: {
        next: function() {
            this.questionIndex++;
            this.clicked = false;
            if (this.questionIndex === this.quiz.questions.length){
                this.startQuiz = false;
            }
        },
        // Go to previous question
        quizScore: function() {
            this.totalQuestions = this.quiz.questions.length,
            this.score = (this.totalCorrectAnswers / this.totalQuestions) * 100
            
            this.score.toFixed(0);
            console.log(this.score);
        },
        start: function (){
            this.startQuiz = true;
            this.questionIndex = 0;
            this.score = 0;
            this.totalCorrectAnswers = 0;
            this.totalWrongAnswers = 0;
        },
        checkAnswer: function (correct){
            this.clicked = true;
            if(correct){
                console.log("helemaal goed");
                this.totalCorrectAnswers++;
                console.log("aantal goede antwoorden: " + this.totalCorrectAnswers);
            } else {    
                console.log("helemaal fout");
                this.totalWrongAnswers++;
                console.log("aantal foute antwoorden: " + this.totalWrongAnswers);
            }
            this.quizScore();
        }
    },
    computed: {
        compClasses: function() {
            return {
                'fa fa-check' : this.faCheck && !this.faTimes,
                'fa fa-times' : this.faTimes && !this.faCheck
            }
        }
    } 
}
</script>

<style scoped>


</style>