<script setup>
import { ref, reactive, onMounted, computed } from 'vue'

const props = defineProps({
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

const firstStyle = reactive(
    props.direction === "row" ? 
        {
            minWidth: props.first_min,
            flexGrow: props.position
        } : {
            minHeight: props.first_min,
            flexGrow: props.position
        }
)   

const first = ref(null)
const second = ref(null)
const container = ref(null)
const splitter = ref(null)
let handling = false
onMounted(() => {
    first.value.style.flexGrow = props.position
    second.value.style.flexGrow = 100 - props.position
    if (props.direction === "row") {
        first.value.style.minWidth = props.first_min
        second.value.style.minWidth = props.second_min
    } else {
        first.value.style.minHeight = props.first_min
        second.value.style.minHeight = props.second_min
    }
    console.log("splitter", splitter.value)
    splitter.value.addEventListener("mousedown", (event) => {
        handling = true
        event.preventDefault()
    })
})

window.addEventListener("mousemove", (event) => {
    if (handling) {   
        console.log("mousemove", handling)
        const { x, y } = container.value.getBoundingClientRect()
        if (props.direction === "row") {
            const left = event.clientX - x
            first.value.style.flexGrow = left
            second.value.style.flexGrow = container.value.clientWidth - left
        } else {
            const top = event.clientY - y
            first.value.style.flexGrow = top
            second.value.style.flexGrow = container.value.clientHeight - top
        }
    }
})
window.addEventListener("mouseup", () => {
    handling = false
})

</script>
<template>
    <div  ref="container" id="container" :class="containerClass">
        <div id="first" ref="first" :class="firstStyle">
            <slot name="first" >fallback first</slot>
        </div>
        <div id="splitter" ref="splitter"></div>
        <div id="second" ref="second" :class="secondStyle">
            <slot name="second" >fallback second</slot>
        </div>
    </div>
</template>
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

