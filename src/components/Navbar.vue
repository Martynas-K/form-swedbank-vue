<template>
    <nav>
        <div class="nav-container">
            <div class="logo"><a href="#">SomeBank</a></div>
            <ul class="links">
                <li><a href="#">Form</a></li>
                <li><a href="#">About Us</a></li>
            </ul>
        </div>
    </nav>
</template>

<script>
    export default {
        name: "Navbar"
    }
</script>

<style scoped>
    nav {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 70px;
        background-color: #ee7023;
    }

    .nav-container {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 10px 0;
        width: 100%;
        max-width: 1200px;
        color: #ffffff;
        font-weight: bold;
    }

    .logo a{
        padding: 10px;
        font-size: 24px;
    }

    .logo :hover {
        background-color: #f4ba44;
        cursor: pointer;
    }

    .links {
        display: flex;
        font-size: 14px;
        color: #ffffff;
    }

    .links li { padding: 10px; }

    .links :hover {
        background-color:  #f4ba44;
        cursor: pointer;
    }

    a { color: #ffffff; }

    @media only screen and (min-width: 425px) {
        nav { height: 100px; }

        .logo a { font-size: 30px; }

        .links { font-size: 18px; }

        .nav-container { padding: 10px 20px; }
    }

</style>