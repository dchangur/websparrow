<template>
    <!-- Navigation-->
    <Navbar />
    <!-- Masthead-->
    <Header />
    <!-- Portfolio Section-->
    <Portfolio />
    <!-- About Section-->
    <About />
    <!-- Contact Section-->
    <Contact />

    <!-- FunQuiz-->
    <FunQuiz />

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
