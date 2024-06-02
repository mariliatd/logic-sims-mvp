<template>
    <div class="nav-container">
        <span class="title">{{ simName }}</span>
        <nav>
            <a class="nav-link" href="#">Ajuda</a>
        </nav>
    </div>
</template>

<script setup lang="ts">
    const props = defineProps({
        simName: { type: String, required: true },
    })
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Fuzzy+Bubbles:wght@400;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Fuzzy+Bubbles:wght@400;700&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

body {
    margin: 0;
}

a {
    text-decoration: none;
    color: inherit;
}

.title {
    font-family: "Fuzzy Bubbles", sans-serif;
    font-size: 2.0rem;
    color: #1D2D44;
    padding: 0.5rem 1.0rem;
}

.nav-container {
    background-color: #86C5E1;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.nav-link {
    font-family: "Roboto", sans-serif;
    font-size: 1.4rem;
    color: #1D2D44;
    padding: 0.5rem 1.0rem;
}
</style>