<script setup lang="ts">
import { computed, onMounted, onUnmounted, reactive, ref } from 'vue'

// page ruler container
const horizontal = ref()
const vertical = ref();
const elemWidth = ref<number>(0);
const elemHeight = ref<number>(0);

const state = reactive({
    dragging: false,
    isHorizontal: false,
});

onMounted(() => {
    updateRulerSize();
    window.addEventListener('resize', updateRulerSize);
});

onUnmounted(() => {
    window.removeEventListener('resize', updateRulerSize);
});

const updateRulerSize = () => {
    console.log('[ updateRulerSize ] >', horizontal.value?.offsetWidth, horizontal.value?.offsetHeight)
    elemWidth.value = horizontal.value?.offsetWidth - 30
    elemHeight.value = vertical.value?.offsetHeight - 30
};

const horizontalMarkArr = computed(() => getMarkArr(elemWidth.value));
const verticalMarkArr = computed(() => getMarkArr(elemHeight.value));

function getMarkArr(elmentLength: number) {
    const markArr = []
    const pixels = 10
    const steps = elmentLength / pixels;
    for (let i = 0; i < steps; i++) {
        const step = i * pixels
        const isMask16 = isMultipleOf100(pixels * i)
        const isMask10 = isMultipleOf50(pixels * i)
        const classList = ['ruler-mark']
        const mark = {
            offsetValue: step + 30,
            classList,
            markValue: ''
        }
        if (isMask16) {
            classList.push(`ruler-mark-16`)
            if (step > 0) {
                mark.markValue = `${step}`;
            }
        } else if (isMask10) {
            classList.push(`ruler-mark-10`)
        } else {
            classList.push(`ruler-mark-6`)
        }

        markArr.push(mark)
    }
    return markArr
}

function isMultipleOf50(num: number): boolean {
    return num % 50 === 0
}
function isMultipleOf100(num: number): boolean {
    return num % 100 === 0
}


let startPosition = 0;
let startSplit = 0;

function dragStart(e: MouseEvent) {

    e.stopPropagation(); // 阻止捕获和冒泡阶段中当前事件的进一步传播
    // e.preventDefault();

    console.log('[ dragStart ] >', e, e.target)
    state.dragging = true;
    const target = e.target as HTMLElement;
    const { type } = target?.dataset;
    state.isHorizontal = type === "horizontal";

    const rulerElement = horizontal.value as HTMLElement;
    console.log('[ target ] >', target, e.pageY, e.pageX)
    // if (target === rulerElement) {

    //     console.log('[ dragStart target horizontal] >', target, horizontal.value, e.pageY, e.pageX)
    //     // if (isLockAdd) {
    //     //     e.stop();
    //     //     return;
    //     // }
    //     const adderElement = document.createElement("div");
    //     adderElement.classList.add(`scale-value`)
    //     rulerElement.append(adderElement)
    //     // datas.fromRuler = true;
    //     // e.target = adderElement;
    //     // add
    // }

    // const target = inputEvent.target;
    // const datas = e.datas;
    // const canvasElement = this.ruler.canvasElement;
    // const guidesElement = this.guidesElement;
    // const isHorizontal = type === "horizontal";
    // const originRect = this.originElement.getBoundingClientRect();
    // const matrix = getDistElementMatrix(this.managerRef.current!);
    // const offsetPos = calculateMatrixDist(matrix, [
    //     e.clientX - originRect.left,
    //     e.clientY - originRect.top,
    // ]);
    // offsetPos[0] -= guidesElement.offsetLeft;
    // offsetPos[1] -= guidesElement.offsetTop;
    // offsetPos[isHorizontal ? 1 : 0] += this.scrollPos * zoom!;

    // datas.offsetPos = offsetPos;
    // datas.matrix = matrix;

    // let isLockAdd = lockGuides && lockGuides.indexOf("add") > -1;
    // let isLockRemove = lockGuides && lockGuides.indexOf("remove") > -1;
    // let isLockChange = lockGuides && lockGuides.indexOf("change") > -1;

    // if (target === canvasElement) {
    //     if (isLockAdd) {
    //         e.stop();
    //         return;
    //     }
    //     datas.fromRuler = true;
    //     datas.target = this.adderElement;
    //     // add
    // } else if (hasClass(target, GUIDE)) {
    //     if (isLockRemove && isLockChange) {
    //         e.stop();
    //         return;
    //     }
    //     datas.target = target;
    //     // change
    // } else {
    //     e.stop();
    //     return false;
    // }


    // if (this.props.useResizeObserver) {
    //     this._observer = new ResizeObserver(this._onCheck);
    //     this._observer.observe(this.guidesElement, {
    //         box: "border-box",
    //     });
    // }
}

function dragMove(e: MouseEvent) {
    if (state.dragging) {
        // const position = state.direction === "horizontal" ? e.pageY : e.pageX;
        console.log('[ dragMove ] >', e.pageY, e.pageX)
        // // const totalSize = isVertical.value
        //     ? container.value.offsetHeight
        //     : container.value.offsetWidth;
        // const dp = position - startPosition;
        // // ~~ 强制转换为整数类型，并且会将小数部分直接截断
        // state.split = startSplit + ~~((dp / totalSize) * 100);
    }
}

function dragEnd() {
    state.dragging = false;
}
</script>
<template>
    <div class="ruler-box"></div>
    <div ref="horizontal" class="ruler ruler-horizontal" data-type="horizontal" @mousedown.prevent="dragStart"
        @mousemove="dragMove" @mouseup="dragEnd">
        <template v-for="item in horizontalMarkArr">
            <div :class="[item.classList]" :style="{ transform: `translateX(` + item.offsetValue + 'px)' }">
                <span class="ruler-mark-value" v-if="item.markValue">{{ item.markValue }}</span>
            </div>
        </template>
        <div class="scena-guides-guides" style="transform: translateY(0px);">
            <div class="scena-guides-display-drag"></div>
            <div class="scena-guides-guide scena-guides-adder"></div>
        </div>
    </div>




    <!-- <div class="__rulerXline" id="__ext_ruler_line"
                        style="width: 100%; height: 10px; background: transparent; position: fixed; z-index: 2147483647; cursor: row-resize; top: 93px;">
                        <div class="__rulerXContent__EL">94 Y<button class="__ruler_delete_line" title="Right Click + Backspace">✕</button>
                        </div>
                    </div> -->
    <div ref="vertical" class="ruler ruler-vertical">
        <template v-for="item in verticalMarkArr">
            <div :class="[item.classList]" :style="{ transform: `translateY(` + item.offsetValue + 'px)' }">
                <span class="ruler-mark-value" v-if="item.markValue">{{ item.markValue }}</span>
            </div>
        </template>
    </div>
    <div class="ruler-container">
        <slot> </slot>
    </div>
</template>

<style>
.__rulerXline {
    left: 0px;
    border: 0.5px solid #0c0e11
}




.scena-guides-guides {
    position: absolute;
    bottom: 0;
    right: 0;
    will-change: transform;
    z-index: 2000;
}

.scena-guides-display-drag {
    position: absolute;
    will-change: transform;
    z-index: 2000;
    font-weight: bold;
    font-size: 12px;
    display: none;
    left: 20px;
    top: -20px;
    color: #f33;
}

.scena-guides-guide-pos {
    position: absolute;
    font-weight: bold;
    font-size: 12px;
    color: #f33;
}

.scena-guides-horizontal .scena-guides-guide-pos {
    bottom: 100%;
    left: 50%;
    transform: translate(-50%);
}

.scena-guides-vertical .scena-guides-guide-pos {
    left: calc(100% + 2px);
    top: 50%;
    transform: translateY(-50%);
}

/* .rCS1g1q24i 
.rCS1g1q24i.scena-guides-horizontal .scena-guides-guides {
    width: 100%;
    height: 0;
}
.rCS1g1q24i.scena-guides-vertical .scena-guides-guides {
    height: 100%;
    width: 0;
}
.rCS1g1q24i .scena-guides-guide {
    position: absolute;
    background: #f33;
    z-index: 2;
}
.rCS1g1q24i .scena-guides-guide.scena-guides-dragging:before {
    position: absolute;
    content: "";
    width: 100%;
    height: 100%;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
.rCS1g1q24i.scena-guides-horizontal .scena-guides-guide {
    width: 100%;
    height: 1px;
    cursor: row-resize;
}
.rCS1g1q24i.scena-guides-vertical .scena-guides-guide {
    width: 1px;
    height: 100%;
    cursor: col-resize;
}
.scena-guides-mobile .rCS1g1q24i.scena-guides-horizontal .scena-guides-guide {
    transform: scale(1, 2);
}
.scena-guides-mobile .rCS1g1q24i.scena-guides-vertical .scena-guides-guide {
    transform: scale(2, 1);
}
.rCS1g1q24i.scena-guides-horizontal .scena-guides-guide:before {
    height: 20px;
}
.rCS1g1q24i.scena-guides-vertical .scena-guides-guide:before {
    width: 20px;
}
.rCS1g1q24i .scena-guides-adder {
    display: none;
}
.rCS1g1q24i .scena-guides-adder.scena-guides-dragging {
    display: block;
} */

.ruler {
    position: absolute;
    top: 0;
    left: 0;
    /* background: rgb(68, 68, 68, 0.2); */
    background: rgba(32, 32, 35, 1);
    z-index: 20;
}

.ruler.ruler-horizontal {
    left: 0px;
    width: 100%;
    height: 30px;

    /* cursor: row-resize; */
    /* pointer-events: auto; */
}

.ruler.ruler-vertical {
    top: 0px;
    width: 30px;
    height: 100%;

    /* cursor: col-resize; */
    /* pointer-events: auto; */
}

.ruler-horizontal .ruler-mark {
    position: absolute;
    width: 1px;
    /* height: 6px; */
    background-color: rgba(127, 127, 127, 1);
}

.ruler-horizontal .ruler-mark-6 {
    top: 24px;
    height: 6px;
}

.ruler-horizontal .ruler-mark-10 {
    top: 20px;
    height: 10px;
}

.ruler-horizontal .ruler-mark-16 {
    top: 14px;
    height: 16px;
}

.ruler-horizontal .ruler-mark-value {
    position: absolute;
    top: -6px;
    left: 4px;
    font-size: 12px;
    color: rgba(127, 127, 127, 1);
}




.ruler-vertical .ruler-mark {
    position: absolute;
    height: 1px;
    background-color: rgba(127, 127, 127, 1);
}

.ruler-vertical .ruler-mark-6 {
    left: 24px;
    width: 6px;
}

.ruler-vertical .ruler-mark-10 {
    left: 20px;
    width: 10px;
}

.ruler-vertical .ruler-mark-16 {
    left: 14px;
    width: 16px;
}

.ruler-vertical .ruler-mark-value {
    position: absolute;
    top: 4px;
    left: -6px;
    font-size: 12px;
    color: rgba(127, 127, 127, 1);
    writing-mode: vertical-rl;
}

/* 左上角的小方块 */
.ruler-box {
    position: relative;
    width: 30px;
    height: 30px;
    background: rgba(32, 32, 35, 1);
    box-sizing: border-box;
    z-index: 21;
}

.ruler-box:before,
.ruler-box:after {
    position: absolute;
    content: '';
    background: #777;
}

.ruler-box:before {
    width: 1px;
    height: 100%;
    left: 100%;
}

.ruler-box:after {
    height: 1px;
    width: 100%;
    top: 100%;
}
</style>
