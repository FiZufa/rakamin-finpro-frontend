<template>
    <div class="header">
        <div class="logo">
            <img src="@/assets/logo.png" alt="logo airbnb">
        </div>
        <div class="menus">
            <button class="dashboard">Dashboard</button>
            <button class="add-btn">+ Rent new room</button>
            <img class="profile" src="@/assets/profile.png" alt="profile img">
        </div>
    </div>

</template>
<script>

</script>
<style>
    html, body {
        margin: 0;
        padding: 0;
        height: 100%;
    }
    .header{
        margin: 0;
        top: 0;
        position: sticky;
        color: #fff;
        background-color: #fff;
        padding: 12px 180px;
        border-bottom: 1px solid #ccc;

        display: flex;
        flex-direction: row;
        align-items: center;
    }

    .logo img {
        height: 60px;
    }

    .logo img:hover {
        cursor: pointer;
    }

    .menus .profile {
        height: 40px;
        border: 1px solid #ccc;
        border-radius: 20px;
    }

    .menus .profile:hover {
        border-color: #ccc; /* Change border color */
        box-shadow: 0 0 4px #ccc; /* Add a soft shadow */
        transform: scale(1.02); /* Slightly enlarge the image */
        transition: all 0.4s ease; /* Smooth transition effect */
        cursor: pointer;
    }

    .menus button {
        height: 30px;
    }

    .menus .dashboard {
        background: none;
        border: none;
        opacity: 0.6;
    }

    .menus .dashboard:hover {
        opacity: 1.0;
        cursor: pointer;
    }

    .menus .add-btn {
        border-radius: 20px;
        border: none;
        padding: 8px 16px;
        background-color: #FF385C;
        color: #fff;
    }

    .menus .add-btn:hover {
        cursor: pointer;
        background-color: #EF2045;
    }

    .menus {
        display: flex;
        flex-direction: row;
        align-items: center;
        flex-wrap: wrap;
        gap: 8px;
        margin-left: auto;
        
    }


</style>