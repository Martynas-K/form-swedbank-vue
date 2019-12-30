<template>
    <div class="question-wrapper">
        <div class="text-wrapper">
            <p>Please review your input data:</p>
        </div>
        <ul class="ul">
            <li class="list">Your first name: {{inputData.enteredFirstName}}</li>
            <li class="list">Your last name: {{inputData.enteredLastName}}</li>
            <li class="list">Type of payment card: {{inputData.pickedCardType}}</li>
            <li v-if="inputData.pickedDebitCardRole" class="list">Your debit card role: {{inputData.pickedDebitCardRole}}</li>
            <li v-if="inputData.pickedCardType === 'Debit'" class="list">Your debit card account: {{inputData.pickedDebitAccount}}</li>
            <li v-if="inputData.pickedCardType === 'Credit'" class="list">Your credit card organisation: {{inputData.pickedCardOrganisation}}</li>
            <li v-if="inputData.pickedCardType === 'Credit'" class="list">Your monthly salary after taxes: {{inputData.enteredSalary}}</li>
            <li v-if="inputData.pickedCreditCardType" class="list">Type of your credit card: {{inputData.pickedCreditCardType}}</li>
            <li class="list">Type of delivery: {{inputData.pickedDeliveryType}}</li>

        </ul>
        <div class="text-wrapper">
            <p>Please click <b><i>submit</i></b> to send this form. We will soon be in touch with you!</p>
        </div>


    </div>
</template>

<script>
    export default {
        name: "QuestionSummary",
        props: ['inputData'],
        data: () => ({

        }),

    }
</script>

<style scoped>
    @import "../../assets/styles/questionIntroSummary.css";

</style>