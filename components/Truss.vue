<script setup>
const props = defineProps({
  width: Number
})
</script>

<template>
    <div :style="{ width: props.width + 'px', height: '29px', backgroundColor: 'blue', textAlign: 'center' }">
        <p>{{ props.width }}</p>
    </div>
</template>
