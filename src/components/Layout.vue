<script setup lang="ts">
import PocketBase from 'pocketbase'
import apiUrl from '../apiUrl';
const pb = new PocketBase(apiUrl);

function logout() {
    pb.authStore.clear()
    localStorage.clear()
}
</script>

<template>
    <div v-if="pb.authStore.model?.email === 'demouser@example.com'" id="demoBanner">You are viewing Lani in demo mode. Data will be static.</div>
    <ul class="navbar">
        <li><RouterLink to="/" class="routerLink">Home</RouterLink></li>
        <li>&nbsp;</li>
        <li><RouterLink to="/about" class="routerLink">About</RouterLink></li>
        <li class="dropdown">
            <a class="dropbtn">{{ pb.authStore.model?.name }} &#9660;</a>
            <div class="dropdown-content">
                <RouterLink to="/account">My Account</RouterLink>
                <RouterLink to="/login" @click="logout">Logout</RouterLink>
            </div>
        </li>
    </ul>

    <slot />
</template>

<style scoped>
.navbar {
    list-style-type: none;
    padding: 0;
    overflow: hidden;
    width: 90%;
    margin: auto;
    text-align: center;
    font-family: 'Poppins', sans-serif;
}

li {
    float: left;
}

li, .dropbtn, .routerLink {
    display: inline-block;
    color: white;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
    font-size: x-large;
}

li.dropdown {
    float: right;
}

.dropdown-content a:hover {
    background-color: lightblue;
    border-radius: 10px;
}

.dropdown-content {
    display: none;
    position: absolute;
    background-color: #f9f9f9;
    min-width: 160px;
    box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
    z-index: 1;
    border-radius: 10px;
}

.dropdown-content a {
    color: black;
    padding: 12px 16px;
    text-decoration: none;
    display: block;
    text-align: left;
}

.dropdown:hover .dropdown-content {
    display: block;
}

#demoBanner {
    width: 100%;
    background-color: red;
    color: white;
    text-align: center;
    font-size: larger;
}
</style>