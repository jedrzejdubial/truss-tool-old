<script setup>
const props = defineProps(['title', 'tag'])

/* Takes tag prop and returns a custom element
Made to work with PhosphorIcons */
function render() {
  return h(props.tag, {size: '32', color: 'white'})
}
</script>

<template>
    <div id="btnWrap">
        <button id="btn">
            <component :is="render" />
        </button>
        <p>{{ props.title }}</p>
    </div>
</template>
