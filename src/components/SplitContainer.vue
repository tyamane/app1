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
<div id="container" ref="container" class="${direction}">

    <div id="first" ref="first" v-bind:style="{'flex-grow': position, minWidth: direction=='row' ? first_min: '100%',minHeight: direction=='row' ? first_min: '100%' }">
        <slot name="first"></slot>
    </div>
    <div id="splitter" ref="splitter"></div>
    <div id="second" ref="second" v-bind:style="{'flex-grow': 100 - position, minWidth: direction=='row' ? second_min: '100%',minHeight: direction=='row' ? second_min: '100%'}">
        <slot name="second"></slot>
    </div>
</div>
</template>
