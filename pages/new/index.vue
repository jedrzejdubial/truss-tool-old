<script setup>
import { PhResize, PhDownloadSimple, PhX } from '@phosphor-icons/vue'
import list from './public/list.json'

const trusses = ref([])

function addTruss(width) {
  trusses.value.push({ width: width })
}

function removeTruss(index) {
  trusses.value.splice(index, 1)
}
</script>

<template>
    <nav>
        <Button title="Show Menu" :tag="PhResize" onclick="list.showModal()" />
        <Button title="Download image" :tag="PhDownloadSimple" />
    </nav>

    <dialog id="list">
        <div id="list_top">
            <h2>Elements</h2>
            <button id="list_close" onclick="list.close()">
                <PhX :size="26" weight="bold" />
            </button>
        </div>

        <div id="list_bottom">
            <ListButton v-for="item in list.items" :item="item" @click="() => addTruss(item.width)" />
        </div>
    </dialog>

    <div id="canvas">
        <Truss v-for="(truss, index) in trusses" :width="truss.width" @remove="removeTruss(index)" :key="index" />
    </div>
</template>

<style>
@import url("~/assets/css/styles.css");

nav {
    display: flex;
    gap: 12px;
    padding: 12px;
}

#list {
    background-color: var(--gray);
    border: none;
    border-radius: 20px;
    padding: 15px;
    width: 60%;
    height: 70%;
    scrollbar-width: none;
}

#list_top {
    display: flex;
    justify-content: space-between;
    align-items: start;
}

#list_close {
    background-color: transparent;
    border-radius: 50px;
    padding: 6px;
    height: 38px;
}

#list_close:hover {
    background-color: #707070;
}

#list_bottom {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    margin-top: 8px;
}
</style>
