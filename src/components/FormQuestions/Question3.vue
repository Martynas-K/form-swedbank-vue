<template>
    <div class="question-wrapper">
        <div class="text-wrapper">Please enter your name and surname to be shown on the card: </div>

        <div class="input-wrapper">
            <p>First name: </p>
                <input class="text-input" type="text" name="FirstName" value="Mickey" placeholder="First name" v-model.lazy="enteredFirstName"><br>
            <p>Last name: </p>
                <input class="text-input" type="text" name="LastName" value="Mouse" placeholder="Last name" v-model.lazy="enteredLastName"><br>
        </div>

        <div v-if="inputData.pickedCardType === 'Debit'" class="input-wrapper">
            <p>Select bank account for your card: </p>
            <div class="select-wrapper">
                <select class="select" id="account" name="account" v-model="pickedDebitAccount">
                    <option value="" disabled selected>Select bank account...</option>
                    <option value="Account 1">LT001111111111111111</option>
                    <option value="Account 2">LT002222222222222222</option>
                    <option value="Account 3">LT003333333333333333</option>
                </select>
            </div>
        </div>

        <div v-if="inputData.pickedCardType === 'Credit'" class="input-wrapper">
            <p>Select card organization: </p>
            <div class="select-wrapper">
                <select class="select" id="cardOrg" name="cardOrg" v-model="pickedCardOrganisation">
                    <option value="" disabled selected>Select card organization...</option>
                    <option value="Mastercard">Mastercard</option>
                    <option value="Visa">Visa</option>
                </select>
            </div>
        </div>

        <div v-if="inputData.pickedCardType === 'Credit'" class="input-wrapper">
            <p>Monthly salary after taxes: </p>
            <input class="text-input" type="text" name="Salary" value="Salary" placeholder="Monthly salary" v-model="enteredSalary"><br>
        </div>

        <div v-show="enteredFirstName && enteredLastName" class="text-wrapper">Thank you, <b>{{enteredFirstName}} {{enteredLastName}}!</b>
            Please click <b><i>next</i></b> for the next step.
        </div>

    </div></template>

<script>
    import { bus } from '../../main';

    export default {
        name: "Question3",
        props: ['inputData'],
        data: () => ({
            enteredFirstName: '',
            enteredLastName: '',
            pickedDebitAccount: '',
            pickedCardOrganisation: '',
            enteredSalary: '',
            error: '',
            errorMessageToggle: false,
        }),

        created:
            function() {
                this.error = 'Please fill all fields.';
                bus.$emit('SetError', {'error': this.error, 'toggle': this.errorMessageToggle});
            },

        updated:
            function() {
                this.errorMessageToggle =
                    this.enteredFirstName && this.enteredLastName &&
                    (this.pickedDebitAccount || (this.pickedCardOrganisation && this.enteredSalary)) ? '' : true;
                this.error = this.enteredFirstName && this.enteredLastName &&
                    (this.pickedDebitAccount || (this.pickedCardOrganisation && this.enteredSalary)) ? '' : 'Please fill all fields';
                bus.$emit('SetError', {'error': this.error, 'toggle': this.errorMessageToggle});
                bus.$emit('SetFirstName', this.enteredFirstName);
                bus.$emit('SetLastName', this.enteredLastName);
                bus.$emit('SetDebitAccount', this.pickedDebitAccount);
                bus.$emit('SetCardOrganisation', this.pickedCardOrganisation);
                bus.$emit('SetSalary', this.enteredSalary);
            },
    }
</script>

<style scoped>

</style>