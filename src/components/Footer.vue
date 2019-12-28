<template>
    <footer>
        <div class="footer-container">© 2019 Copyright: SomeBank</div>
    </footer>
</template>

<script>
    export default {
        name: "Footer"
    }
</script>

<style scoped>
    footer {
        position : absolute;
        bottom : 0;
        margin-top : 50px;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 50px;
        background-color: #512b2b;
    }

    .footer-container {
        display: flex;
        flex-direction: row-reverse;
        justify-content: right;
        padding: 10px;
        width: 100%;
        max-width: 1200px;
        font-size: 14px;
        color: #ffffff;
    }


    @media only screen and (min-width: 425px) {
        footer {
            height: 70px;
        }

        .footer-container {
            padding: 10px 30px;
            font-size: 18px;
        }
    }
</style>