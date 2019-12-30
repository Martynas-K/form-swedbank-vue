<template>
    <div class="question-wrapper">
        <div class="text-wrapper">Please select the role of your card: </div>
        <div class="radio-wrapper">
            <input type="radio" id="main" value="Main" v-model="pickedDebitCardRole">
            <label for="main">Main card</label>
            <p class="description">The main card is for you.</p>
            <br>
            <input type="radio" id="supplementary" value="Supplementary" v-model="pickedDebitCardRole">
            <label for="supplementary">Supplementary card</label>
            <p class="description">You can order additional card for your family members or other persons which will be connected to the same account and they will be able to use the funds in your bank account.</p>
            <br>
        </div>
        <div v-show="pickedDebitCardRole" class="text-wrapper">You have selected a <b>{{ pickedDebitCardRole }} card</b>. Please click
            <b><i>next</i></b> to continue.
        </div>
    </div>
</template>

<script>
    import { bus } from '../../main';

    export default {
        name: "Question2Debit",
        data: () => ({
            pickedDebitCardRole: '',
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
                this.errorMessageToggle = this.pickedDebitCardRole ? '' : true;
                this.error = this.pickedDebitCardRole ? '' : 'Please fill all fields';
                bus.$emit('SetError', {'error': this.error, 'toggle': this.errorMessageToggle});
                bus.$emit('SetDebitCardRole', this.pickedDebitCardRole);

            },
    }
</script>

<style scoped>
    @import "../../assets/styles/question1_2.css";
</style>