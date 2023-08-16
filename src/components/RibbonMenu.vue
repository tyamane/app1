<script setup>
import { ref, reactive, onMounted, computed } from 'vue'
import Menu from './Menu.vue'


</script>
<template>
    <div class="tabs" >
        <li v-on:click="change('1')" v-bind:class="{'active': isActive === '1'}">タブ1</li>
        <li v-on:click="change('2')" v-bind:class="{'active': isActive === '2'}">タブ2</li>
        <li v-on:click="change('3')" v-bind:class="{'active': isActive === '3'}">タブ3</li>
    </div>
    <div class="ribbon">
        <slot name="ribbon" >fallback ribbon</slot>
    </div>
</template>
<style>
* {
    box-sizing: border-box;
}
.selected{
    background: #707d8a;
}
.menubar{
    height: 1.5em;
    width: 30px;

    background: gray;
    border: 1px solid #aaa;
    border-radius: 5px;
    padding: 0.5em;
    margin: 0.5em;

    justify-content: center;
    align-items: center;
    cursor: pointer;
}

</style>

