<script setup>
const props = defineProps({
  title: String,
  tag: Object,
  path: String,
  action: Function
})

/* Takes tag prop and returns a custom element
Made to work with PhosphorIcons */
const IconComponent = () => h(props.tag, { size: '32', color: 'white' })
</script>

<template>
    <div id="button_wrap">
        <button id="button_el" @click="navigateTo(props.path)">
            <component :is="IconComponent" />
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
