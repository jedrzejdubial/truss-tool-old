<script setup>
import { PhFilePlus, PhFolderOpen } from '@phosphor-icons/vue'
</script>

<template>
    <div id="wrap">
        <h1>Welcome to Truss Tool</h1>
        <div id="buttons">
            <Button title="Create a new project" :tag="PhFilePlus" />
            <Button title="Open an existing project" :tag="PhFolderOpen" />
        </div>
    </div>
</template>

<style>
@import url("~/assets/css/styles.css");
</style>
