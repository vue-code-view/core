<script setup lang="ts">
function isMultipleOf50(num: number): boolean {
    return num % 50 === 0
}
function isMultipleOf100(num: number): boolean {
    return num % 100 === 0
}
const vRuler = {
    mounted: (el, binding) => {

        var container = document.querySelector(".ruler-container") as HTMLElement;
        console.log('[ containerElm ] >', container.offsetWidth, container.offsetHeight)

        const direction = binding.arg
        const ruler = document.createElement('div')
        ruler.classList.add('ruler')
        ruler.classList.add(`ruler-${direction}`)
        const pixels = binding.value || 5
        // console.log('[ window.screen ] >', window.screen, binding)
        const screenKey = direction === 'horizontal' ? 'width' : 'height'
        const screenRange = direction === 'horizontal' ? container.offsetWidth / pixels : container.offsetHeight / pixels
        console.log('[ screenRange ] >', screenRange)
        for (let i = 0; i < screenRange; i++) {
            const step = i * pixels
            // console.log('[ direction ] >', i)
            const mark = document.createElement('div')
            const isMask16 = isMultipleOf100(pixels * i)
            const isMask10 = isMultipleOf50(pixels * i)
            mark.classList.add(`ruler-mark`)
            if (isMask16) {
                mark.classList.add(`ruler-${direction}-mark-16`)
                if (step > 0) {
                    const text = document.createElement('span')
                    text.classList.add(`scale-value`)
                    text.innerText = `${step}`
                    mark.appendChild(text)
                }
            } else if (isMask10) {
                mark.classList.add(`ruler-${direction}-mark-10`)
            } else {
                mark.classList.add(`ruler-${direction}-mark-6`)
            }

            mark.style[direction === 'horizontal' ? 'left' : 'top'] = `${step}px`
            ruler.appendChild(mark)
        }
        el.appendChild(ruler)
    }
}
</script>
<template>
    <div class="ruler-container" v-ruler:horizontal="5" v-ruler:vertical="5">
        <!-- v-ruler:vertical="10" -->
        <!-- <div class="ruler-horizontal"></div>
                                                                                                                                                                                                                                                                                                                                                    <div class="ruler-vertical"></div> -->
        <slot></slot>
    </div>
</template>

<style>
.ruler {
    position: absolute;
    z-index: 9999;
    width: 100%;
    height: 100%;
    pointer-events: none;
}

.ruler-container {
    position: relative;
}

/* 水平刻度尺 */
.ruler-horizontal {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    background-image: repeating-linear-gradient(to bottom,
            #ccc,
            #ccc 1px,
            transparent 1px,
            transparent);
    z-index: 9999;
    background-color: rgba(32, 32, 35, 1);
}

.ruler-horizontal .ruler-mark {
    position: absolute;
    width: 1px;
    background-color: #ccc;
}

.ruler-horizontal .ruler-mark .scale-value {
    position: absolute;
    top: -6px;
    left: 4px;
    font-size: 12px;
    color: #909399;
}

.ruler-horizontal-mark-6 {
    top: -6px;
    height: 6px;
}

.ruler-horizontal-mark-10 {
    top: -10px;
    height: 10px;
}

.ruler-horizontal-mark-16 {
    top: -16px;
    height: 16px;
}

/* 垂直刻度尺 */
.ruler-vertical {
    position: absolute;
    top: 0;
    left: 0;
    width: 10px;
    /* 刻度尺宽度 */
    height: 100%;
    background-image: repeating-linear-gradient(to right,
            #ccc,
            #ccc 1px,
            transparent 1px,
            transparent);
    background-color: rgba(32, 32, 35, 1);

    z-index: 9999;
}

.ruler-vertical .ruler-mark {
    position: absolute;
    height: 1px;
    /* 刻度线宽度 */
    background-color: #ccc;
    /* 刻度线颜色 */
}

.ruler-vertical .ruler-mark .scale-value {
    position: absolute;
    top: 4px;
    left: -6px;
    font-size: 12px;
    color: #909399;
    writing-mode: vertical-rl;
}

.ruler-vertical-mark-6 {
    left: -6px;
    width: 6px;
}

.ruler-vertical-mark-10 {
    left: -10px;
    width: 10px;
}

.ruler-vertical-mark-16 {
    left: -16px;
    width: 16px;
}
</style>
