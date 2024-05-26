<template>
  <div id="testAl2">
    <el-container>
      <el-aside width="200px">
        <el-collapse accordion>
          <el-collapse-item name="1">
            <template #title>
              数组<el-icon class="header-icon">
                <info-filled />
              </el-icon>
            </template>
            <div>
              Consistent with real life: in line with the process and logic of real
              life, and comply with languages and habits that the users are used to;
            </div>
            <div>
              Consistent within interface: all elements should be consistent, such
              as: design style, icons and texts, position of elements, etc.
            </div>
          </el-collapse-item>

          <el-collapse-item title="二叉树" name="2">
          </el-collapse-item>

          <el-collapse-item title="链表" name="3">
          </el-collapse-item>

          <el-collapse-item title="栈" name="4">
          </el-collapse-item>

          <el-collapse-item title="文字" name="5">
            <el-button @click="addIText">文字</el-button>
          </el-collapse-item>

          <el-collapse-item title="代码块" name="6">
          </el-collapse-item>
        </el-collapse>
      </el-aside>
      <el-container>
        <el-header>Header</el-header>
        <el-main><canvas ref="domCanvas"></canvas></el-main>
        <el-footer>Footer</el-footer>
      </el-container>
    </el-container>

  </div>
</template>

<script lang="ts" setup>
import { onMounted, ref, type Ref } from "vue";
import { fabric } from "fabric";

const domCanvas: Ref<HTMLCanvasElement | null> = ref(null);
const canvas = ref<fabric.Canvas>();
const circle = ref<fabric.Circle>();


onMounted(() => {
  init();
  draw();
});

function init() {
  canvas.value = new fabric.Canvas(domCanvas.value, {
    width: 1280,
    height: 1000,
    backgroundColor: "#e3fdfd",
  });
}

function draw() {
  circle.value = new fabric.Circle({
    left: 100,
    top: 100,
    radius: 50,
    stroke: "black",
    fill: "red",
  });
  canvas.value?.add(circle.value);
}

function addIText() {
  const itext = ref<fabric.IText>();
  itext.value = new fabric.IText("", {
    fontFamily: 'Comic Sans',
    fontSize: 20
  });
  canvas.value?.add(itext.value);
  canvas.value?.setActiveObject(itext.value);
  itext.value.enterEditing();
}

canvas.value?.on('mouse:wheel', function (opt) {
  let delta = opt.e.deltaY;
  let zoom = canvas.value?.getZoom();
  if (zoom) {
    zoom *= 0.999 ** delta;
    if (zoom > 20) zoom = 20;
    if (zoom < 0.01) zoom = 0.01;
  }
  canvas.value?.setZoom(zoom as number);
  opt.e.preventDefault();
  opt.e.stopPropagation();
})

</script>

<style scoped>
canvas {
  width: 1000px;
}
</style>