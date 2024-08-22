<script setup>
import { PhDownloadSimple, PhFileArrowDown, PhSelection, PhArrowClockwise, PhTrashSimple } from '@phosphor-icons/vue'
import list from './public/list.json'
</script>

<template>
    <nav>
        <div id="new_buttons">
            <Button :tag="PhDownloadSimple" />
            <Button :tag="PhFileArrowDown" />
            <Button :tag="PhSelection" />
            <Button :tag="PhArrowClockwise" />
            <Button :tag="PhTrashSimple" />
        </div>

        <div id="new_info">
            <h2>[] connectors</h2>
            <h2>Elements list:</h2>
        </div>
    </nav>

    <div id="new_list">
        <h2>Elements</h2>
        <div v-for="item in list.items" :key="item.id">
            <h3>{{ item.title }}</h3>
            <p>{{ item.width }}cm</p>
        </div>
    </div>

    <div class="canvas">
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
    margin-top: 0;
}

#new_buttons {
    display: flex;
    gap: 12px;
}

#new_info {
    display: flex;
    gap: 100px;
}

#new_list {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background-color: var(--gray);
    border-radius: 0 12px 12px 0;
    padding: 15px;
    width: 30px;
    height: 70%;

    transition-property: width;
    transition-duration: 400ms;
    transition-timing-function: ease;
}

#new_list > * {
    display: none;
}

#new_list:hover {
    width: 330px;
    overflow: scroll;
    scrollbar-width: none;
}

#new_list:hover > * {
    display: block;
}
</style>
