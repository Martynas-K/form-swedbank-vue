<template>
    <div class="form-wrapper">
        <form>
            <div class="step-header-container">
                <div class="step-header-title">{{formData[step].stepTitle}}</div>
                <div class="step-header-content">{{formData[step].stepContent}}</div>
            </div>
            <div class="question-heading">{{formData[step].questionText}}</div>
            <div class="question-input-container">
                <keep-alive>
                    <component :is="dynamicComponent" v-bind:inputData = 'inputData'></component>
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
    import formData from '../assets/data/formData';
    import { bus } from '../main'

    export default {
        name: "FormTemplate",
        components: {},
        data: () => ({
            formData,
            error: '',
            errorMessageToggle: false,
            step: 0,
            finalStepIndex: 1,
            inputData: {
                pickedCardType: '',
                pickedDebitCardRole: '',
                pickedCreditCardType: '',
                pickedDeliveryType: '',
                enteredFirstName: '',
                enteredLastName: '',
                pickedDebitAccount: '',
            },
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
                alert('Your form has been submitted! Somewhere. Probably...');
            },
        },

        created:
            function () {
                return this.finalStepIndex = formData.length - 1;
            },

        updated:
            function () {
                bus.$on('SetError', (data) => {
                    this.error = data.error;
                    this.errorMessageToggle = data.toggle;
                });
                bus.$on('SetCardType', (data) => { this.inputData.pickedCardType = data; });
                bus.$on('SetDebitCardRole', (data) => { this.inputData.pickedDebitCardRole = data; });
                bus.$on('SetCreditCardType', (data) => { this.inputData.pickedCreditCardType = data; });
                bus.$on('SetDeliveryType', (data) => { this.inputData.pickedDeliveryType = data; });
                bus.$on('SetFirstName', (data) => { this.inputData.enteredFirstName = data; });
                bus.$on('SetLastName', (data) => { this.inputData.enteredLastName = data; });
                bus.$on('SetDebitAccount', (data) => { this.inputData.pickedDebitAccount = data; });
                bus.$on('SetCardOrganisation', (data) => { this.inputData.pickedCardOrganisation = data; });
                bus.$on('SetSalary', (data) => { this.inputData.enteredSalary = data; });

            },

        computed: {
            dynamicComponent() {
                //TODO replace with switch
                let component = "";
                if (this.step === 0) {
                    component = "QuestionIntro";
                } else if (this.step === this.finalStepIndex) {
                    component = "QuestionSummary";
                } else if (this.step === 2) {
                    component = 'Question' + this.step + this.inputData.pickedCardType;
                } else {
                    component = 'Question' + this.step;
                }
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