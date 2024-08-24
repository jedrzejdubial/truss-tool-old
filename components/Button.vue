<script setup>
const props = defineProps({
  title: String,
  tag: Object,
  path: String,
  action: Function
})

const handleClick = computed(() => {
  return props.action ? props.action : props.path ? () => navigateTo(props.path) : undefined
})
</script>

<template>
    <button :title="props.title" @click="handleClick">
        <component :is="() => h(props.tag, { size: '32', color: 'white' })" />
    </button>
</template>

<style scoped>
button {
    width: 60px;
    height: 60px;
    padding: 15px;
    border-radius: 8px;
    background-color: var(--gray);
}
</style>
