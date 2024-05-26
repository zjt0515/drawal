<template>
  <div>
    <canvas width="400" height="400" id="canvas" style="border: 1px solid #ccc;"></canvas>
  </div>
</template>

<script setup lang="ts">
import { onMounted } from 'vue'
import { fabric } from 'fabric'

// 初始化
function init() {
  const canvas = new fabric.Canvas('canvas', {
    isDrawingMode: true, // 开启绘图模式
  })

  // 设置画笔颜色
  canvas.freeDrawingBrush.color = '#11999e'

  // 设置画笔粗细
  canvas.freeDrawingBrush.width = 10

  // 画笔投影
  canvas.freeDrawingBrush.shadow = new fabric.Shadow({
    blur: 10,
    offsetX: 10,
    offsetY: 10,
    affectStroke: true,
    color: '#30e3ca',
  })
}

const props = defineProps({

})
onMounted(() => {
  init()
})
</script>
