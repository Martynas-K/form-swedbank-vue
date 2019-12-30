<template>
    <div class="question-wrapper">
        <div class="text-wrapper">Please select your card delivery method: </div>
        <div class="select-wrapper">
            <select class="select" id="country" name="country" v-model="pickedDeliveryType">
                <option value="" disabled selected>Select your option...</option>
                <option value="by post">Via post</option>
                <option value="at Vilnius branch">Vilnius, SomeBank's branch Street 1</option>
                <option value="at Kaunas branch">Kaunas, SomeBank's branch Street 2</option>
                <option value="at Klaipėda branch">Klaipėda, SomeBank's branch Street 3</option>
                <option value="at Šiauliai branch">Šiauliai, SomeBank's branch Street 4</option>
                <option value="at Panevėžys branch">Panevėžys, SomeBank's branch Street 5</option>
            </select>
        </div>
        <div v-show="pickedDeliveryType" class="text-wrapper">You have selected the card to be delivered <b>{{ pickedDeliveryType }}.</b>
            Please click <b><i>next</i></b> for the final step of this form!
        </div>
    </div>
</template>

<script>
    import { bus } from '../../main';

    export default {
        name: "Question4",
        data: () => ({
            pickedDeliveryType: '',
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
                this.errorMessageToggle = this.pickedDeliveryType ? '' : true;
                this.error = this.pickedDeliveryType ? '' : 'Please fill all fields';
                bus.$emit('SetError', {'error': this.error, 'toggle': this.errorMessageToggle});
                bus.$emit('SetDeliveryType', this.pickedDeliveryType);
            },
    }
</script>

<style scoped>
    @import "../../assets/styles/questions.css";
</style>