<script setup>
import { ref, reactive, onMounted, computed } from 'vue'


</script>
<template>
    <div class="menu" >
        <slot name="menu" >fallback menu</slot>
    </div>
</template>
<style>
* {
    box-sizing: border-box;
}
.selected{
    background: #707d8a;
}
.menu{
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

