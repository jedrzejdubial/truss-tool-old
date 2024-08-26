<script setup>
import { PhArrowClockwise, PhTrashSimple } from '@phosphor-icons/vue'

const props = defineProps({
  width: Number
})

const emit = defineEmits(['remove'])

const hidden = ref('hidden')
const rotation = ref(0)

function toggleHidden() {
  hidden.value = hidden.value === '' ? 'hidden' : ''
}

function rotate() {
  rotation.value += 90
}

function remove() {
  // Hides truss_actions on delete
  toggleHidden()
  emit('remove')
}
</script>

<template>
    <div :style="{ width: props.width + 'px', transform: `rotate(${rotation}deg)` }">
        <div class="truss_actions">
            <Button title="Rotate" :tag="PhArrowClockwise" width="29" height="29" iconSize="15" :class="hidden" @click="rotate" />
            <Button title="Remove" :tag="PhTrashSimple" width="29" height="29" iconSize="15" :class="hidden" @click="remove" />
        </div>

        <div class="truss" @click.right.prevent="toggleHidden">
            <p>{{ props.width }}</p>
        </div>
    </div>
</template>

<style scoped>
.truss_actions {
    height: 29px;
    display: flex;
    justify-content: center;
    gap: 10px;
}

.truss {
    height: 29px;
    background-color: gray;
    text-align: center;
}

p {
    margin: 0;
}

.hidden {
    display: none;
}
</style>
