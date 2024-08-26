<script setup>
const props = defineProps({
  item: Object
})
</script>

<template>
    <button>
        <img :src="'/truss/' + props.item.id + '.jpg'" />
        <div>
            <h2>{{ props.item.title }}</h2>
            <p>{{ props.item.width }}x29cm</p>
            <p>{{ props.item.weight }}kg</p>
        </div>
    </button>
</template>

<style scoped>
button {
    display: flex;
    background-color: transparent;
    margin: 8px;
}

img {
    border-radius: 10px;
}

div {
    text-align: left;
    padding-left: 8px;
}

p {
    margin: 4px 0 0 0;
}
</style>
