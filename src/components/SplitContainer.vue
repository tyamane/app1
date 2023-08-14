<script setup>
defineProps({
  direction: {
    type: String,
    required: true
  },
  position: {
    type: Number,
    default: 50
  },
  first_min:{
    type: Number,
    default: 0
  },
  second_min:{
    type: Number,
    default: 0
  }, 
})



</script>

<style>
* {
    box-sizing: border-box;
}
#container {
    width: 100%;
    height: 100%;
    display: flex;
}
.column {
    flex-flow: column;
}
.row {
    flex-flow: row;
}
#splitter {
    min-width:3px;
    min-height: 3px;
    background: silver;
}
.row #splitter {
    cursor: col-resize;
}
.column #splitter {
    cursor: row-resize;
}
#splitter:hover {
    background: deepskyblue;
}
#first,#second {
    flex: 1 0 0;
    overflow: auto;
}
</style>
<template>

<div v-if="direction=='row'" id="container" class="row">
    <div id="first" v-bind:style="{'flex-grow': position, minWidth: first_min}">
        <slot name="first" >fallback first</slot>
    </div>
    <div id="splitter" ref="splitter"></div>
    <div id="second" v-bind:style="{'flex-grow': 100-position, minWidth: second_min}">
        <slot name="second" >fallback second</slot>
    </div>
</div>
<div v-else id="container" class="column">
    <div id="first" v-bind:style="{'flex-grow': position, minHeight: first_min}">
        <slot name="first" >fallback first</slot>
    </div>
    <div id="splitter" ref="splitter"></div>
    <div id="second" v-bind:style="{'flex-grow': 100-position, minHeight: second_min}">
        <slot name="second" >fallback second</slot>
    </div>
</div>
</template>
