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
    import formData from '../assets/formData';
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

    .stepper-wrapper {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin: 20px 10px;
        width: 100%;
        max-width: 1200px;
        background-color: antiquewhite;
        min-height: 80px;
    }


    .stepper-item-container {
        display: flex;
        flex: 1;
        align-items: center;
    }

    .stepper-item {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 40px;
        min-width: 40px;
        background-color: #ee7023;
        border-radius: 20px;
        font-weight: bold;
        color: #ffffff;
    }

    .stepper-divider-bar {
        display: none;
    }

    .stepper-item-container:last-child {
        max-width: 40px;
    }

    .stepper-item-container:last-child .stepper-divider-bar{
        display: none;
    }

    .stepper-wrapper:first-child {
        margin-left: 0;
    }

    .stepper-wrapper:last-child {
        margin-right: 0;
    }

    .stepper-hide-long {
        display: none;
    }

    .stepper-active {
        background-color: #f4ba44;
    }

    /*adjust min-width if more steps are added*/
    @media only screen and (min-width: 720px) {
        .stepper-hide-short {
            display: none;
        }

        .stepper-hide-long {
            display: flex;
            min-width: 95px;
        }

        .stepper-item-container:last-child {
            max-width: 95px;
        }

        .stepper-divider-bar {
            display: flex;
            margin: 0 10px;
            background-color: #ee7023;
            width: 100%;
            min-width: 4px;
            height: 4px;
            border-radius: 3px;
        }
    }

</style>