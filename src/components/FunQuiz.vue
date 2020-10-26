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

                    <div class="row mt-3" v-show="startQuiz || score >= 0">
                        <div class="col-md-12" >
                            <p class="text-primary  animatedEnd animatedFadeInUp fadeInUpEnd" v-if="score >= 55 && questionIndex === quiz.questions.length">
                                Looks like we should grab a cup of coffee! <br> Just call me. My treat!<br>
                                 <i class=" animatedEnd animatedFadeInUp fadeInUpEnd fa fa-smile fa-5x text-primary mt-2"></i>
                                
                            </p>
                            <p class="text-danger animatedEnd animatedFadeInUp fadeInUpEnd" v-if="score < 55 && questionIndex === quiz.questions.length">
                                Looks like we're not really a match eh..?<br>
                                But you may still contact me, maybe we could work something out?<br>
                                <i class=" animatedEnd animatedFadeInUp fadeInUpEnd fa fa-frown fa-5x text-danger mt-2"></i>
                            </p>
                        </div>

                        
                    </div>

                    <button v-show="!startQuiz" class=" animatedEnd animatedFadeInUp fadeInUpEnd btn btn-lg btn-primary" v-on:click="start">Find out if we are a match</button>

                    <div class="" v-for="(question, index) in quiz.questions" :key="index">
                        <div class="row" v-show="index === questionIndex && startQuiz"> 
                            <div class="col-md-12 mb-md-5 mb-2">
                                <div >
                                    <h3 class="text-primary mb-2" >{{question.text}}</h3>
                                </div>
                            </div>
                            <div class="mb-md-5 mb-2" v-for="(response, index) in question.responses" :key="response" v-bind:class="{ 'col-md-6': question.responses.length <= 2, 'col-md-4': question.responses.length >= 3 }" >

                               <div class="mb-md-5 mb-2 mr-4">
                                    <div class="animated animatedFadeInUp fadeInUp" v-show="response.correct && clicked && (UserAnswer === response.index)">
                                        <i class="fa fa-thumbs-up fa-2x text-success text-center absolute"></i>
                                    </div>
                                    <div class="animated animatedFadeInUp fadeInUp" v-show="!response.correct && clicked && (UserAnswer === response.index)">
                                        <i class="fa fa-thumbs-down fa-2x text-danger  text-center absolute"></i>
                                    </div>
                               </div>

                               <div class="">
                                    <button v-bind:disabled="clicked" v-bind:value="response.correct" class="col-md-12 btn btn-lg" 
                                        v-bind:class="{ [btnDanger] : !response.correct && clicked && (UserAnswer === response.index), [btnSucess] : response.correct  && clicked && (UserAnswer === response.index), [btnOutline] : !clicked || UserAnswer != response.index}" v-on:click="checkAnswer(response.correct, index)">
                                        {{response.text}}   
                                    </button>
                               </div>

                            </div>
                            <div v-if="clicked" class="col-md-12 mb-2">
                                <button class="btn btn-primary" v-bind:disabled="!clicked" v-on:click="next">
                                   <span v-if="questionIndex === quiz.questions.length - 1"> See results </span>
                                   <span v-else> Next question </span>
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
        {text: 'Hell yeah', correct: true, index: 0}, 
        {text: 'Not sure', correct: true, index: 1}, 
        {text: 'Nope', correct: false, index: 2}, 
      ]
    }, {
      text: "Do you need help with a webproject?",
      responses: [
        {text: 'Hell yeah', correct: true, index: 0}, 
        {text: 'Maybe', correct: true, index: 1}, 
        {text: 'Nope', correct: false, index: 2}, 
      ]
    }, 
    {
      text: "How many years experience should your candidate have at least?",
      responses: [
        {text: '1 year', correct: true, index: 0}, 
        {text: '1 - 3 years', correct: true, index: 1}, 
        {text: '+3 years', correct: false, index: 2}, 
      ]
    },
    {
      text: "Do you prefer to work with mentally strong people",
      responses: [
        {text: 'Hell yeah', correct: true, index: 0}, 
        {text: 'Maybe', correct: true, index: 1}, 
        {text: 'Nope', correct: false, index: 2}, 
      ]
    }, {
      text: "What do you think of working 9 to 5?",
      responses: [
        {text: 'Exactly how i like it', correct: false, index: 0}, 
        {text: 'Thats old fashion', correct: true, index: 1}, 
        {text: 'Not enaugh hours', correct: true, index: 2}, 
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
       score: 0,
       UserAnswer: 0,
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
        checkAnswer: function (correct, index){
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
            this.UserAnswer = index;
      

        }
    }
}
</script>

<style scoped>

.absolute{
position: absolute;

}

.relative{
 position: relative;
}

/* Animation */

@keyframes fadeInUp {
    from {
        transform: translate3d(0,40px,0)
    }

    to {
        transform: translate3d(0,0,0);
        
    }
    0%,100% { opacity: 0; }
    20% { opacity: 1; }
}

@-webkit-keyframes fadeInUp {
    from {
        transform: translate3d(0,40px,0)
    }

    to {
        transform: translate3d(0,0,0);
        
    }
    0%,100% { opacity: 0; }
    20% { opacity: 1; }
}


@keyframes fadeInUpEnd {
    from {
        transform: translate3d(0,40px,0)
    }

    to {
        transform: translate3d(0,0,0);
        opacity: 1
    }

}

@-webkit-keyframes fadeInUpEnd {
    from {
        transform: translate3d(0,40px,0)
    }

    to {
        transform: translate3d(0,0,0);
        opacity: 1
    }

}




.animated {
    animation-duration: 0.6s;
    animation-fill-mode: both;
    -webkit-animation-duration: 0.6s;
    -webkit-animation-fill-mode: both;
}

.animatedEnd {
    animation-duration: 2s;
    animation-fill-mode: both;
    -webkit-animation-duration: 2s;
    -webkit-animation-fill-mode: both;
}

.animatedFadeInUp {
    opacity: 0
}

.fadeInUp {
    opacity: 0;
    animation-name: fadeInUp;
    -webkit-animation-name: fadeInUp;
}

.fadeInUpEnd {
    opacity: 0;
    animation-name: fadeInUpEnd;
    -webkit-animation-name: fadeInUpEnd;
}

</style>