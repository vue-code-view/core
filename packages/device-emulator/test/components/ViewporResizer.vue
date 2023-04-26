<template>
    <div class="container" :style="{ width: containerWidth + 'px', height: containerHight + 'px' }">

        <slot name="content"></slot>
        <div class="handle right" @mousedown="onMouseDown($event, 'right')"></div>
        <div class="handle bottom" @mousedown="onMouseDown($event, 'bottom')"></div>
        <div class="handle corner" @mousedown="onMouseDown($event, 'corner')"></div>
    </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
    name: 'ResizableContainer',
    setup(props) {
        const container = ref(null);
        const handle = ref(null);
        const width = ref(props.width);
        const height = ref(props.height);
        const startX = ref(0);
        const startY = ref(0);

        function onMouseDown(event, type) {
            handle.value = event.target;
            startX.value = event.clientX;
            startY.value = event.clientY;

            window.addEventListener('mousemove', onMouseMove);
            window.addEventListener('mouseup', onMouseUp);
            // event.preventDefault();
        }

        function onMouseMove(event) {
            // event.preventDefault()
            // event.stopPropagation();
            if (!handle.value) {
                return;
            }
            const dx = (event.clientX - startX.value) * 1.5;
            const dy = event.clientY - startY.value;
            if (handle.value.classList.contains('right')) {
                width.value += dx;
            }
            if (handle.value.classList.contains('bottom')) {
                height.value += dy;
            }
            if (handle.value.classList.contains('corner')) {
                width.value += dx;
                height.value += dy;
            }
            startX.value = event.clientX;
            startY.value = event.clientY;

            console.log('onMouseMove', startX.value, startY.value, width.value, height.value);
        }

        function onMouseUp() {
            handle.value = null;
            window.removeEventListener('mousemove', onMouseMove);
            window.removeEventListener('mouseup', onMouseUp);
        }

        const containerWidth = computed(() => width.value < 52 ? 52 : width.value);
        const containerHight = computed(() => height.value < 52 ? 52 : height.value);

        return {
            container,
            width,
            height,
            onMouseDown,
            containerWidth,
            containerHight
        }
    },
    props: {
        width: {
            type: Number,
            required: true
        },
        height: {
            type: Number,
            required: true
        }
    }
}
</script>

<style>
.container {
    position: relative;
    border: 1px solid #ccc;
    overflow: hidden;
}

.handle {
    position: absolute;
    background-color: #f0f0f0;
}

.right {
    top: 0;
    bottom: 0;
    right: -3px;
    width: 5px;
    cursor: ew-resize;
}

.bottom {
    left: 0;
    right: 0;
    bottom: -3px;
    height: 5px;
    cursor: ns-resize;
}

.corner {
    right: -3px;
    bottom: -3px;
    width: 10px;
    height: 10px;
    cursor: nwse-resize;
}
</style>
