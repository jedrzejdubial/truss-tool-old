<script setup>
import html2canvas from 'html2canvas'
import { PhPlus, PhListNumbers, PhDownloadSimple } from '@phosphor-icons/vue'
import list from './public/list.json'

const trusses = ref([])
let nextId = 0

const parentTruss = ref(null)
const selectedSide = ref(null)

function addTruss(item) {
  trusses.value.push({ ...item, id: nextId++, x: 25, y: 75 /* Default position */ })
  listDialog.close()

  // Remove .startProject welcome screen
  document.querySelector('#canvas').classList.remove('center')
  document.querySelector('.startProject').remove()
}

function removeTruss(id) {
  const index = trusses.value.findIndex(truss => truss.id === id)
  if(index !== -1) trusses.value.splice(index, 1)
}

const trussCount = computed(() => {
  const counts = {}
  trusses.value.forEach(truss => {
    counts[truss.title] = (counts[truss.title] || 0) + 1
  })
  return Object.entries(counts)
    .sort(([a], [b]) => a.localeCompare(b))
    .map(([title, count]) => `${count}x ${title}`)
})

async function download() {
  const canvas = document.querySelector('#canvas')

  try {
    const image = await html2canvas(canvas)
    const link = document.createElement('a')

    link.download = 'truss_tool-image.png'
    link.href = image.toDataURL('image/png')
    link.click()
  } catch(error) {
    console.error(error)
  }
}

function openListDialog(trussId, side) {
  // Get parent element
  parentTruss.value = trusses.value.find(t => t.id === trussId)

  selectedSide.value = side
  listDialog.showModal()
}

function addAdjacentTruss(item) {
  if(parentTruss.value && selectedSide.value) {
    const index = trusses.value.findIndex(t => t.id === parentTruss.value.id)
    const newTruss = { ...item, id: nextId++ }

    if(selectedSide.value === 'left') {
      newTruss.x = parentTruss.value.x - item.width - 16
      newTruss.y = parentTruss.value.y
      trusses.value.splice(index, 0, newTruss)
    } else if(selectedSide.value === 'right') {
      newTruss.x = parentTruss.value.x + parentTruss.value.width + 16
      newTruss.y = parentTruss.value.y
      trusses.value.splice(index + 1, 0, newTruss)
    }

    // Close dialog after picking truss
    listDialog.close()

    // Clear out the data
    parentTruss.value = null
    selectedSide.value = null
  }
}
</script>

<template>
    <nav>
        <Button title="Show details" :tag="PhListNumbers" onclick="details.showModal()" />
        <Button title="Download an image of current canvas" :tag="PhDownloadSimple" @click="download" /> <!-- Doesn't work on Linux, works on Mac (???) -->
    </nav>

    <div id="canvas" class="center">
        <div class="startProject center">
            <Button title="Add truss" :tag="PhPlus" onclick="listDialog.showModal()" />
            <p>Start your project by adding the first truss</p>
        </div>

        <Truss
            v-for="truss in trusses"
            :width="truss.width"
            :x="truss.x" :y="truss.y"
            @remove="removeTruss(truss.id)"
            @addAdjacent="({ side, id }) => openListDialog(id, side)"
            :id="truss.id"
            :key="truss.id" />
    </div>

    <Dialog title="Elements" id="listDialog">
        <div id="list_bottom">
            <ListButton
                v-for="(item, index) in list.items"
                :item="item"
                @click="() => parentTruss ? addAdjacentTruss(item) : addTruss(item)"
                :key="index" />
        </div>
    </Dialog>

    <Dialog title="Details" id="details">
        <p v-for="(item, index) in trussCount" :key="index">{{ item }}</p>
    </Dialog>
</template>

<style>
@import url("~/assets/css/styles.css");

nav {
    display: flex;
    gap: 12px;
    padding: 12px;
}

#list_bottom {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    margin-top: 8px;
}

#canvas {
  background-color: var(--black);
  height: calc(100vh - 88px);
}

.center {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
</style>
