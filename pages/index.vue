<script setup>
import { PhFilePlus } from '@phosphor-icons/vue'
</script>

<template>
    <div id="main_wrap">
        <h1>Welcome to Truss Tool</h1>
        <Button title="Create a new project" :tag="PhFilePlus" path="/new" />
    </div>
</template>

<style>
@import url("~/assets/css/styles.css");

#main_wrap {
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    box-sizing: border;
}
</style>
