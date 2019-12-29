<template>
    <div class="question-wrapper">
        <div class="text-wrapper">Please select the type of payment card you would like to order: </div>
        <div class="radio-wrapper">
            <input type="radio" id="debit" value="Debit" v-model="picked">
            <label for="debit">Debit card</label>
            <br>
            <input type="radio" id="credit" value="Credit" v-model="picked">
            <label for="credit">Credit card</label>
            <br>

        </div>
        <div v-show="picked" class="text-wrapper">You have selected a <b>{{ picked }} card</b>. Please click
            <b><i>next</i></b> to continue.
        </div>



    </div>
</template>

<script>
    import { bus } from '../../main';

    export default {
        name: "Question1",
        data: () => ({
            picked: '',
            error: '',
            errorMessageToggle: false,
        }),

        created:
            function() {
                this.error = '[default] Please fill all fields';
                bus.$emit('AddError', {'error': this.error, 'toggle': this.errorMessageToggle});
            },

        updated:
            function() {
                this.errorMessageToggle = this.picked ? '' : true;
                this.error = this.picked ? '' : 'Please fill all fields';
                bus.$emit('AddError', {'error': this.error, 'toggle': this.errorMessageToggle});
            },

        }
</script>

<style scoped>
    @import "../../assets/styles/question1.css";
</style>