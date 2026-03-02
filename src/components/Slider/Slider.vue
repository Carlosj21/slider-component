<template>
    <div class="slider">
        <canvas
            ref="canvas"
            class="slider-canvas"
            width="640"
            height="400"
        />
        <aside>Drag to change image</aside>
    </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const props = defineProps({
    imageUrls: { type: Array, default: () => [] }
});

const canvas = ref(null);
const ctx = ref(null);
const images = ref([]);
const offsetX = ref(0);
const totalWidth = ref(0);
const isDragging = ref(false);
const lastX = ref(0);

function fitImage(img) {
    const ratio = img.width / img.height;
    const canvasRatio = 640 / 400;
    const scale = ratio >= canvasRatio ? 640 / img.width : 400 / img.height;
    const w = img.width * scale;
    const h = img.height * scale;
    const x = (640 - w) / 2;
    const y = (400 - h) / 2;
    return { img, x, y, w, h };
}

function loadImages() {
    let loaded = 0;
    images.value = new Array(props.imageUrls.length);
    props.imageUrls.forEach((url, index) => {
        const img = new Image();
        img.crossOrigin = 'anonymous';
        img.onload = () => {
            images.value[index] = fitImage(img);
            loaded++;
            if (loaded === props.imageUrls.length) {
                totalWidth.value = props.imageUrls.length * 640;
                render();
            }
        };
        img.src = url;
    });
}

function render() {
    if (!ctx.value) return;
    ctx.value.fillStyle = '#f2f2f2';
    ctx.value.fillRect(0, 0, 640, 400);

    const startImg = Math.max(0, Math.floor(offsetX.value / 640));
    const endImg = Math.min(props.imageUrls.length, startImg + 2);
    const localOffset = offsetX.value % 640;

    for (let i = startImg; i < endImg; i++) {
        const data = images.value[i];
        if (data) {
            const x = 640 * (i - startImg) - localOffset;
            ctx.value.drawImage(data.img, data.x + x, data.y, data.w, data.h);
        }
    }
}

function startDrag(e) {
    isDragging.value = true;
    lastX.value = e.pageX;
    e.preventDefault();
}

function move(e) {
    if (!isDragging.value) return;
    const deltaX = lastX.value - e.pageX;
    offsetX.value += deltaX;
    offsetX.value = Math.max(0, Math.min(offsetX.value, totalWidth.value - 640));
    lastX.value = e.pageX;
    render();
}

function endDrag() {
    isDragging.value = false;
}

onMounted(() => {
    const el = canvas.value;
    ctx.value = el.getContext('2d');
    loadImages();

    el.addEventListener('mousedown', startDrag);
    document.addEventListener('mousemove', move);
    document.addEventListener('mouseup', endDrag);
});

onUnmounted(() => {
    const el = canvas.value;
    el && el.removeEventListener('mousedown', startDrag);
    document.removeEventListener('mousemove', move);
    document.removeEventListener('mouseup', endDrag);
});
</script>

<style scoped>
.slider {
    font-family: Arial, sans-serif;
    text-align: center;
}

.slider-canvas {
    margin: 20px auto;
    outline: 1px solid #ccc;
    cursor: grab;
    width: 640px;
    height: 400px;
}

aside {
    color: #999;
    font-size: 14px;
}
</style>