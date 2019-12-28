<template>
    <div class="form-wrapper">
        <form>
            <div class="step-header-container">
                <div class="step-header-title">{{formData[step].stepTitle}}</div>
                <div class="step-header-content">{{formData[step].stepContent}}</div>
            </div>
            <div class="question-text">{{formData[step].questionText}}</div>
            <div class="question-input-container">
                <Question1></Question1>
            </div>
            <div class="buttons-container">
                <button v-if="step !== finalStepIndex" @click.prevent="next()">Next</button>
                <button v-if="step === finalStepIndex" @click.prevent="submit()">Submit</button>
                <button v-if="step > 0" @click.prevent="prev()">Previous</button>
            </div>
        </form>
    </div>
</template>


<script>
    /* eslint-disable no-console */

    import formData from '../assets/formData';
    import Question1 from "./Question1";

    export default {
        name: "FormTemplate",
        components: {Question1},
        data: () => ({
            formData,
            step: 0,
            finalStepIndex: 1,
        }),

        methods: {
            prev() {
                this.step--;
            },
            next() {
                this.step++;
            },
            submit() {
                alert('Submit to blah and show blah and etc.');
            },
        },
        created:
            function () {
                return this.finalStepIndex = formData.length - 1;
            }
    }
</script>

<style scoped>
    form {
    }

    .form-wrapper {
        overflow: auto;
        height: 100%;
        min-height: 400px;
        width: 100%;
        max-width: 1200px;
        background-color: antiquewhite;
    }

    .step-header-container {
        display: flex;
        /*box-sizing: border-box;*/
        height: 40px;
        width: 100%;
        min-width: 325px;
        border-radius: 20px;
        border: solid #f4ba44 2px;
        font-weight: bold;

    }

    .step-header-title {
        display: flex;
        justify-content: center;
        /*padding-left: 10px;*/
        line-height: 32px;
        height: 100%;
        width: 120px;
        border-radius: 20px;
        border: solid #f4ba44 2px;
        background-color: #f4ba44;
        color: #ffffff;
    }

    .step-header-content {
        display: flex;
        padding-left: 10px;
        line-height: 36px;
        color: #ee7023;
    }

    .question-text {
        padding: 20px;
        color: #512b2b;
        font-weight: bold;
    }

    .buttons-container {
        display: flex;
        flex-direction: row-reverse;
        justify-content: space-between;
        width: 100%;
        height: 40px;
        padding: 20px;
        color: #ffffff;
        font-weight: bold;
        font-size: 14px;
    }

    button {
        height: 30px;
        width: 120px;
        background-color: #f4ba44;
        border-radius: 20px;
        border: solid #f4ba44 2px;
        outline: none;
    }

    button:hover {
        background-color: #ee7023;
        border: #ee7023;
    }

    .question-input-container {
        width: 100%;
        height: 200px;
        background-color: burlywood;
    }

</style>