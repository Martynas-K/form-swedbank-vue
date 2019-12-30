<template>
    <div class="question-wrapper">
        <div class="text-wrapper">
            <p>Please review your input data:</p>
        </div>
        <ul class="ul">
            <li class="list">Type of payment card: {{inputData.pickedCardType}}</li>
            <li v-if="inputData.pickedDebitCardRole" class="list">Role of your debit card: {{inputData.pickedDebitCardRole}}</li>
            <li v-if="inputData.pickedCreditCardType" class="list">Type of your credit card: {{inputData.pickedCreditCardType}}</li>

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