<template>
    <div class="stepper-wrapper">
        <div class="stepper-item-container" v-for="item in formData" :key="item.id">
            <div class="stepper-item stepper-hide-short" :class="getActiveStepperClass(item.id)">{{item.stepTitleShort}}</div>
            <div class="stepper-item stepper-hide-long" :class="getActiveStepperClass(item.id)">{{item.stepTitle}}</div>
            <div class="stepper-divider-bar"></div>
        </div>
    </div>
</template>

<script>
    import formData from '../assets/data/formData';
    import { bus } from '../main';

    export default {
        name: "Stepper",
        data: () => ({
            formData,
            step: 0,
        }),
        created:
            function () {
            bus.$on('ChangeStep', (data) => {
                this.step = data;
                // eslint-disable-next-line no-console
                console.log('Step changed to: ' + this.step)
            })
        },
        methods: {
            getActiveStepperClass(id) {
                return this.step === id - 1 ? 'stepper-active' : '';
            }
        }

    }
</script>

<style scoped>
    @import "../assets/styles/stepper.css";
</style>