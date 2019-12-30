<template>
    <div class="question-wrapper">
        <div class="text-wrapper">Please select your credit card type: </div>
        <div class="radio-wrapper">
            <input type="radio" id="fixed" value="Fixed payment" v-model="pickedCreditCardType">
            <label for="fixed">Fixed payment credit card</label>
            <p class="description">Works like instalments: useful for bigger purchases or unforeseen expenses.</p>
            <br>
            <input type="radio" id="revolving" value="Revolving" v-model="pickedCreditCardType">
            <label for="revolving">Revolving credit card</label>
            <p class="description">Best choice for your purchases and occasional travels abroad.</p>
            <br>
            <input type="radio" id="gold" value="Gold revolving " v-model="pickedCreditCardType">
            <label for="gold">Gold revolving credit card</label>
            <p class="description">Gives you travel insurance for the whole family and protects most of your purchases.</p>
            <br>
            <input type="radio" id="platinum" value="Visa Platinum" v-model="pickedCreditCardType">
            <label for="platinum">Visa Platinum credit card</label>
            <p class="description">SomeBank's best travel insurance, unlimited access to lounges and rental car insurance.</p>
            <br>
        </div>
        <div v-show="pickedCreditCardType" class="text-wrapper">You have selected a <b>{{ pickedCreditCardType }} card</b>. Please click
            <b><i>next</i></b> to continue.
        </div>
    </div>
</template>

<script>
    import { bus } from '../../main';

    export default {
        name: "Question2Credit",
        data: () => ({
            pickedCreditCardType: '',
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
                this.errorMessageToggle = this.pickedCreditCardType ? '' : true;
                this.error = this.pickedCreditCardType ? '' : 'Please fill all fields';
                bus.$emit('SetError', {'error': this.error, 'toggle': this.errorMessageToggle});
                bus.$emit('SetCreditCardType', this.pickedCreditCardType);
            },
    }
</script>

<style scoped>
    @import "../../assets/styles/questions.css";
</style>