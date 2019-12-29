<template>
    <div class="form-wrapper">
<!--        <form @submit="checkForm">-->
        <form>
            <div class="step-header-container">
                <div class="step-header-title">{{formData[step].stepTitle}}</div>
                <div class="step-header-content">{{formData[step].stepContent}}</div>
            </div>
            <div class="question-heading">{{formData[step].questionText}}</div>
            <div class="question-input-container">
                <keep-alive>
                    <component :is="dynamicComponent"></component>
                </keep-alive>
            </div>
            <div v-if="errorMessageToggle" class="error">{{error}}</div>
            <div class="buttons-container">
                <button class="btn" v-if="step !== finalStepIndex" @click.prevent="next()">Next</button>
                <button class="btn" v-if="step === finalStepIndex && !isError" @click.prevent="submitForm()">Submit</button>
                <button class="btn btn-flex" v-if="step > 0" @click.prevent="prev()">Previous</button>
            </div>
        </form>
    </div>
</template>


<script>
    /* eslint-disable no-console */
    import formData from '../assets/data/formData';
    import { bus } from '../main'

    export default {
        name: "FormTemplate",
        components: {},
        data: () => ({
            formData,
            step: 0,
            finalStepIndex: 1,
            error: '',
            errorMessageToggle: false,
        }),

        methods: {
            prev() {
                if (!this.error) {
                    this.step--;
                    bus.$emit('ChangeStep', this.step);
                } else {
                    this.errorMessageToggle = true;
                }
            },
            next() {
                if (!this.error) {
                    this.step++;
                    bus.$emit('ChangeStep', this.step);
                } else {
                    this.errorMessageToggle = true;
                }
            },
            submitForm() {
                alert('Your form has been submitted, probably...');
            },
        },

        created:
            function () {
                return this.finalStepIndex = formData.length - 1;
            },

        updated:
            function () {
                bus.$on('AddError', (data) => {
                    this.error = data.error;
                    this.errorMessageToggle = data.toggle;
                    // eslint-disable-next-line no-console
                    console.log('Error changed to: ' + this.error)
                });
                return this.error;
            },

        computed: {
            dynamicComponent() {
                let component = "";
                if (this.step === 0) {
                    component = "QuestionIntro";
                } else if (this.step === this.finalStepIndex) {
                    component = "QuestionSummary";
                } else {
                    component = 'Question' + this.step;
                }
                console.log('dynamiccomp error: ', this.error);
                return () => import(`../components/FormQuestions/${component}.vue`);
            },
            isError() {
                return !!this.error;
            }
        }
    }
</script>

<style scoped>
    @import '../assets/styles/formTemplate.css';
</style>