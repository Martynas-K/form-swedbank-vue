<template>
  <div class="page-container">
    <Navbar></Navbar>
    <div class="form-container">
      <Stepper></Stepper>
      <FormTemplate></FormTemplate>
    </div>
    <Footer></Footer>
  </div>
</template>

<script>
import Navbar from './components/Navbar';
import Stepper from './components/Stepper';
import FormTemplate from "./components/FormTemplate";
import Footer from "./components/Footer";

export default {
  name: 'App',

  components: {
    Navbar,
    Stepper,
    FormTemplate,
    Footer,
  },

  data: () => ({
    //
  }),
};
</script>

<style>
  * {
    box-sizing: border-box;
    text-decoration: none;
    list-style: none;
    font-family: sans-serif;
  }

  .page-container {
    position: relative;
    height: 100%;
    min-height: 100vh;
  }

  .form-container {
    display: flex;
    flex-flow: column;
    height: 100%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 10px 10px 70px 10px;
  }

</style>
