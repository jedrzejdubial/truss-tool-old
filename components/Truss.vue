<script setup>
import { PhArrowClockwise, PhTrashSimple } from '@phosphor-icons/vue'

const props = defineProps({
  width: Number
})

const emit = defineEmits(['remove'])

const hidden = ref('hidden')
const rotation = ref(0)
const position = ref({ x: 100, y: 100 })
const isDragging = ref(false)
const startPosition = ref({ x: 0, y: 0 })

function toggleActions() {
  hidden.value = hidden.value === '' ? 'hidden' : ''
}

function rotate() {
  rotation.value += 90
}

function remove() {
  // Hides truss_actions on delete
  toggleActions()
  emit('remove')
}

function startDrag(event) {
  isDragging.value = true
  startPosition.value = { x: event.clientX - position.value.x, y: event.clientY - position.value.y }
}

function onDrag(e) {
  if(isDragging.value) position.value = { x: e.clientX - startPosition.value.x, y: e.clientY - startPosition.value.y }
}

function stopDrag() {
  isDragging.value = false
}
</script>

<template>
    <div :style="{
      width: props.width + 'px',
      transform: `rotate(${rotation}deg)`,
      position: 'absolute',
      left: `${position.x}px`,
      top: `${position.y}px` }">
        <div class="actions">
            <Button title="Rotate" :tag="PhArrowClockwise" width="29" height="29" iconSize="15" :class="hidden" @click="rotate" />
            <Button title="Remove" :tag="PhTrashSimple" width="29" height="29" iconSize="15" :class="hidden" @click="remove" />
        </div>

        <div
            class="element"
            :style="{ cursor: isDragging ? 'grabbing' : 'grab' }"
            @click.right.prevent="toggleActions"
            @mousedown.prevent="startDrag"
            @mousemove.prevent="onDrag"
            @mouseup.prevent="stopDrag"
            @mouseleave.prevent="stopDrag">
            <p>{{ props.width }}</p>
        </div>
    </div>
</template>

<style scoped>
.actions {
    height: 29px;
    display: flex;
    justify-content: center;
    gap: 10px;
}

.element {
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
