<script setup>
import { PhResize, PhDownloadSimple, PhSelection, PhArrowClockwise, PhTrashSimple, PhX } from '@phosphor-icons/vue'
import list from './public/list.json'
</script>

<template>
    <nav>
        <div id="new_buttons">
            <Button title="Show Menu" :tag="PhResize" onclick="list.showModal()" />
            <Button title="Download image" :tag="PhDownloadSimple" />
            <Button title="Deselect truss" :tag="PhSelection" />
            <Button title="Rotate truss" :tag="PhArrowClockwise" />
            <Button title="Delete truss" :tag="PhTrashSimple" />
        </div>

        <div id="new_info">
            <h2>[] connectors</h2>
            <h2>Elements list:</h2>
        </div>
    </nav>

    <dialog id="list">
        <div id="list_top">
            <h2>Elements</h2>
            <button id="list_close" onclick="list.close()">
                <PhX :size="26" color="#fff" weight="bold" />
            </button>
        </div>

        <div id="list_bottom">
            <ListButton v-for="item in list.items" :item="item" />
        </div>
    </dialog>

    <div id="canvas">
        <Truss v-for="item in list.items" :width="item.width" />
    </div>
</template>

<style>
@import url("~/assets/css/styles.css");

nav {
    display: flex;
    justify-content: space-between;
    padding: 12px;
}


#new_buttons {
    display: flex;
    gap: 12px;
}

#new_info {
    display: flex;
    gap: 100px;
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
