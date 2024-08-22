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
    <div id="button_wrap">
        <button id="button_el" @click="handleClick">
            <component :is="() => h(props.tag, { size: '32', color: 'white' })" />
        </button>
        <p>{{ props.title }}</p>
    </div>
</template>

<style scoped>
#button_wrap {
    display: flex;
    flex-direction: column;
    align-items: center;
}

#button_el {
    width: 60px;
    height: 60px;
    padding: 15px;
    border: none;
    border-radius: 8px;
    background-color: var(--gray);
    cursor: pointer;
}
</style>
