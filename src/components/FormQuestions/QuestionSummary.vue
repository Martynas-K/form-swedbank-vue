<template>
    <div class="question-wrapper">
        <div class="text-wrapper">
            <p>Please review your input data:</p>
        </div>
        <ul class="ul">
            <li class="list">Type of payment card: {{inputData.pickedCardType}}</li>

        </ul>
        <div class="text-wrapper">
            <p>Please click <b><i>submit</i></b> to send this form. We will soon be in touch with you!</p>
        </div>


    </div></template>

<script>
    export default {
        name: "QuestionSummary",
        props: ['inputData'],
        data: () => ({

        }),

    }
</script>

<style scoped>
    @import "../../assets/styles/questionSummary.css";

</style>