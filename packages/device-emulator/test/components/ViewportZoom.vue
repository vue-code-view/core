<template>
    <div class="viewport-zoom">
        <div class="viewport-wrapper" :style="wrapperStyle" ref="wrapperRef">
            <div class="viewport" :style="viewportStyle"></div>
            <div class="handle" :style="handleStyle" @mousedown.prevent="startDrag" @mousemove="handleDrag"
                @mouseup="stopDrag" @mouseleave="stopDrag" ref="handleRef"></div>
        </div>
    </div>
</template>
<!-- ViewportZoom -->
<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'


export interface Props {
    width: number;
    height: number;
    handleSize: number;
    minScale: number;
    maxScale: number;
    scaleStep: number;

}
// const props = defineProps<{
//     width: number
//     height: number
//     disableScaling: boolean
// }>()
const props = withDefaults(defineProps<Props>(), {
    width: 1024,
    height: 768,
    handleSize: 20,
    minScale: 0.1,
    maxScale: 10,
    scaleStep: 0.1,
});

const wrapperRef = ref()
const handleRef = ref()
const dragging = ref(false)
const lastX = ref(0)
const lastY = ref(0)
const scaleX = ref(1)
const scaleY = ref(1)

const wrapperStyle = computed(() => ({
    width: `${props.width}px`,
    height: `${props.height}px`,
    overflow: 'hidden',
    position: 'relative',
}))

const viewportStyle = computed(() => ({
    width: `${props.width}px`,
    height: `${props.height}px`,
    transform: `scale(${scaleX.value}, ${scaleY.value})`,
    transformOrigin: 'top left',
}))

const handleStyle = computed(() => ({
    width: `${props.handleSize}px`,
    height: `${props.handleSize}px`,
    borderRadius: `${props.handleSize}px`,
    backgroundColor: 'rgba(0, 0, 0, 0.5)',
    position: 'absolute',
    right: 0,
    bottom: 0,
    cursor: 'se-resize',
}))

const startDrag = (event) => {
    console.log('startDrag', event)
    event.preventDefault()
    dragging.value = true
    lastX.value = event.clientX
    lastY.value = event.clientY
}

const stopDrag = () => {
    console.log('stopDrag')

    dragging.value = false
}

const handleDrag = (event) => {
    console.log('handleDrag', event)

    if (!dragging.value) {
        return
    }

    const deltaX = event.clientX - lastX.value
    const deltaY = event.clientY - lastY.value

    const newWidth = Math.max(
        props.width * scaleX.value + deltaX,
        props.handleSize,
    )
    const newHeight = Math.max(
        props.height * scaleY.value + deltaY,
        props.handleSize,
    )

    scaleX.value = newWidth / props.width
    scaleY.value = newHeight / props.height

    lastX.value = event.clientX
    lastY.value = event.clientY
}

const handleWheel = (event) => {
    console.log('handleWheel', event)

    event.preventDefault()

    const delta = event.deltaY < 0 ? -props.scaleStep : props.scaleStep
    const newScaleX = scaleX.value + delta
    const newScaleY = scaleY.value + delta

    scaleX.value = Math.min(
        Math.max(newScaleX, props.minScale),
        props.maxScale,
    )
    scaleY.value = Math.min(
        Math.max(newScaleY, props.minScale),
        props.maxScale,
    )
}

onMounted(() => {
    // window.addEventListener('mousemove', handleDrag)
    // window.addEventListener('mouseup', stopDrag)
    // handleRef.value.addEventListener('mousedown', startDrag)
    // wrapperRef.value.addEventListener('wheel', handleWheel)
})

</script>

<style scoped>
/* viewport-zoom 组件样式 */
.viewport-zoom {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
}

.viewport-zoom .viewport-wrapper {
    position: relative;
    width: 100%;
    height: 100%;
    max-width: 800px;
    max-height: 600px;
    margin: 0 auto;
    border: 1px solid #ccc;
    overflow: hidden;
}

.viewport-zoom .viewport {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    transform-origin: bottom right;
    transition: transform 0.2s ease-out;
}

.viewport-zoom .handle {
    position: absolute;
    right: -10px;
    bottom: -10px;
    width: 20px;
    height: 20px;
    border: 1px solid #ccc;
    border-radius: 50%;
    background-color: #fff;
    cursor: nwse-resize;
    transition: all 0.2s ease-out;
}

.viewport-zoom .handle:hover {
    border-color: #aaa;
}

.viewport-zoom .handle:active {
    transform: scale(1.2);
}
</style>