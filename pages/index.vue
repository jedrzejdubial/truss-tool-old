<script setup>
import { PhFilePlus } from '@phosphor-icons/vue'
</script>

<template>
    <div>
        <h1>Welcome to Truss Tool</h1>
        <Button :tag="PhFilePlus" path="/new" />
        <p>Create a new project</p>
    </div>
</template>

<style scoped>
@import url("~/assets/css/styles.css");

div {
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
</style>
