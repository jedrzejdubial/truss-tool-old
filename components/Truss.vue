<script setup>
import { PhArrowClockwise, PhTrashSimple } from '@phosphor-icons/vue'

const props = defineProps({
  width: Number
})

const emit = defineEmits(['remove'])

const hidden = ref('hidden')
const rotation = ref(0)
const position = ref({ x: 25, y: 75 })

function toggleActions() {
  hidden.value = hidden.value === '' ? 'hidden' : ''
}

function rotate() {
  rotation.value += 90
}

function remove() {
  // Hides truss_actions on delete
  toggleActions()
  // Uses :remove emit to get function for removing truss
  emit('remove')
}

function edge() {
  list.showModal()
}
</script>

<template>
    <div :style="{
      width: props.width + 40 + 'px',
      transform: `rotate(${rotation}deg)`,
      position: 'absolute',
      left: `${position.x}px`,
      top: `${position.y}px` }">
        <div class="actions">
            <Button title="Rotate" :tag="PhArrowClockwise" :width="29" :height="29" :iconSize="15" :class="hidden" @click="rotate" />
            <Button title="Remove" :tag="PhTrashSimple" :width="29" :height="29" :iconSize="15" :class="hidden" @click="remove" />
        </div>

        <div class="element_wrap" :style="{ width: props.width + 40 + 'px' }">
            <div class="edge" @click="edge"></div>
            <div
                class="element"
                :style="{ width: props.width + 'px' }"
                @click.right.prevent="toggleActions">
              <p>{{ props.width }}</p>
            </div>
            <div class="edge" @click="edge"></div>
        </div>
    </div>
</template>

<style scoped>
.element_wrap {
  display: flex;
  cursor: pointer;
}

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

.edge {
  background-color: pink;
  width: 20px;
}

.hidden {
    display: none;
}
</style>
