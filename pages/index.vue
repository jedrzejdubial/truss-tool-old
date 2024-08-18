<script setup>
import { PhFilePlus, PhFolderOpen } from '@phosphor-icons/vue'
</script>

<template>
    <div id="main_wrap">
        <h1>Welcome to Truss Tool</h1>
        <div id="main_buttons">
            <Button title="Create a new project" :tag="PhFilePlus" :path="'/new'" />
            <Button title="Open an existing project" :tag="PhFolderOpen" />
        </div>
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

#main_buttons {
    display: flex;
    gap: 50px;
}
</style>
