<script setup>
const props = defineProps({
  width: String
})
</script>

<template>
    <div :style="{ width: props.width + 'px', height: '29px', backgroundColor: 'blue', textAlign: 'center' }">
        <p>{{ props.width }}</p>
    </div>
</template>
