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
  @import "./assets/styles/app.css";
</style>
