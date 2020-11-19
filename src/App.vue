<template>
    <!-- Navigation-->
    <Navbar />
    <!-- Masthead-->
    <Header />
    <!-- About Section-->
    <About />
    <!-- Portfolio Section-->
    <Portfolio />
    <!-- FunQuiz-->
    <FunQuiz />
    <!-- Contact Section-->
    <Contact />
    <!-- Footer-->
    <Footer />
</template>

<script>
  import Portfolio from './components/Portfolio.vue'
  import Navbar from './components/Navbar'
  import About from './components/About'
  import Header from './components/Header'
  import Contact from './components/Contact'
  import Footer from './components/Footer'
  import FunQuiz from './components/FunQuiz'

  export default {
    name: 'App',
    components: {
      Portfolio,
      Navbar,
      About,
      Header,
      Contact,
      Footer,
      FunQuiz
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
