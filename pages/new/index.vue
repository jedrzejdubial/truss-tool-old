<script setup>
import { PhResize, PhListNumbers } from '@phosphor-icons/vue'
import list from './public/list.json'

const trusses = ref([])
let nextId = 0

function addTruss(item) {
  trusses.value.push({ ...item, id: nextId++ })
}

function removeTruss(id) {
  const index = trusses.value.findIndex(truss => truss.id === id)
  if(index !== -1) trusses.value.splice(index, 1)
}

const trussCount = computed (() => {
  const counts = {}
  trusses.value.forEach(truss => {
    counts[truss.title] = (counts[truss.title] || 0) + 1
  })
  return Object.entries(counts)
    .sort(([a], [b]) => a.localeCompare(b))
    .map(([title, count]) => `${count}x ${title}`)
})
</script>

<template>
    <nav>
        <Button title="Show menu" :tag="PhResize" onclick="list.showModal()" />
        <Button title="Show details" :tag="PhListNumbers" onclick="details.showModal()" />
    </nav>

    <div id="canvas">
        <Truss v-for="truss in trusses" :width="truss.width" @remove="removeTruss(truss.id)" :key="truss.id" />
    </div>

    <Dialog title="Elements" id="list">
        <div id="list_bottom">
            <ListButton v-for="(item, index) in list.items" :item="item" @click="() => addTruss(item)" :key="index" />
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
</style>
