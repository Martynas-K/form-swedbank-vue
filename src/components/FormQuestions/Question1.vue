<template>
    <div class="question-wrapper">
        <div class="text-wrapper">Please select the type of payment card you would like to order: </div>
        <div class="radio-wrapper">
            <input type="radio" id="debit" value="Debit" v-model="pickedCardType">
            <label for="debit">Debit card</label>
            <br>
            <input type="radio" id="credit" value="Credit" v-model="pickedCardType">
            <label for="credit">Credit card</label>
            <br>

        </div>
        <div v-show="pickedCardType" class="text-wrapper">You have selected a <b>{{ pickedCardType }} card</b>. Please click
            <b><i>next</i></b> to continue.
        </div>



    </div>
</template>

<script>
    import { bus } from '../../main';

    export default {
        name: "Question1",
        data: () => ({
            pickedCardType: '',
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
                this.errorMessageToggle = this.pickedCardType ? '' : true;
                this.error = this.pickedCardType ? '' : 'Please fill all fields';
                bus.$emit('SetError', {'error': this.error, 'toggle': this.errorMessageToggle});
                bus.$emit('SetCardType', this.pickedCardType);

            },

        }
</script>

<style scoped>
    @import "../../assets/styles/question1.css";
</style>