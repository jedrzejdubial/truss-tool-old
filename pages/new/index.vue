<script setup>
import { PhResize, PhDownloadSimple, PhSelection, PhArrowClockwise, PhTrashSimple, PhX } from '@phosphor-icons/vue'
import list from './public/list.json'
</script>

<template>
    <nav>
        <div id="new_buttons">
            <Button :tag="PhResize" onclick="list.showModal()" />
            <Button :tag="PhDownloadSimple" />
            <Button :tag="PhSelection" />
            <Button :tag="PhArrowClockwise" />
            <Button :tag="PhTrashSimple" />
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

        <div v-for="item in list.items" :key="item.id">
            <h3>{{ item.title }}</h3>
            <p>{{ item.width }}cm</p>
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
    padding: 12px;
    justify-content: space-between;
}

h2 {
    margin: 0;
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
    color: white;
    border: none;
    border-radius: 12px;
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
    border: none;
    border-radius: 50px;
    padding: 6px;
    height: 38px;
    cursor: pointer;
}

#list_close:hover {
    background-color: #707070;
}
</style>
