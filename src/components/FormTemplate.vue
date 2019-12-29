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
                    <component :is="dynamicComponent"></component>
                </keep-alive>
            </div>
            <div class="buttons-container">
                <button class="btn" v-if="step !== finalStepIndex" @click.prevent="next()">Next</button>
                <button class="btn" v-if="step === finalStepIndex" @click.prevent="submit()">Submit</button>
                <button class="btn" v-if="step > 0" @click.prevent="prev()">Previous</button>
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
        // components: {},
        data: () => ({
            formData,
            step: 0,
            finalStepIndex: 1,
        }),

        methods: {
            prev() {
                this.step--;
                bus.$emit('ChangeStep', this.step);
            },
            next() {
                this.step++;
                bus.$emit('ChangeStep', this.step);
            },
            submit() {
                alert('Submit to blah and show blah and etc.');
            },
        },
        created:
            function () {
                return this.finalStepIndex = formData.length - 1;
            },

        computed: {
            dynamicComponent() {
                console.log('sadsdsaasdsd', this.step)
                let component = "";
                if (this.step === 0) {
                    component = "QuestionIntro";
                } else if (this.step === this.finalStepIndex) {
                    component = "QuestionSummary";
                } else {
                    component = 'Question' + this.step;
                }

                return () => import(`../components/FormQuestions/${component}.vue`);
            },
        }
    }
</script>

<style scoped>
    @import '../assets/styles/formTemplate.css';
</style>