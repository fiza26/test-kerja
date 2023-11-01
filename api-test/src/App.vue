<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Poppins&display=swap" rel="stylesheet">
  <header>
    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: 'Poppins', sans-serif;
  background-color: #dddd;
}
a {
  color: white;
  text-decoration: none;
}
nav {
  display: flex;
  align-items: center;
  justify-content: space-around;
  background-color: #6c5ce7;
  padding: 7px;
  height: 50px;
}
</style>
