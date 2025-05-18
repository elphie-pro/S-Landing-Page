<template>
  <figure
    ref="cardRef"
    class="relative w-full h-full flex flex-col items-center justify-center"
    :style="{
      height: containerHeight,
      width: containerWidth,
      perspective: '800px'
    }"
    @mousemove="handleMouse"
    @mouseenter="handleMouseEnter"
    @mouseleave="handleMouseLeave"
  >
    <div v-if="showMobileWarning" class="absolute top-4 text-center text-sm block sm:hidden">
      This effect is not optimized for mobile. Check on desktop.
    </div>
    
    <div
      class="relative"
      :style="{
        width: imageWidth,
        height: imageHeight,
        transform: `rotateX(${rotateXValue}deg) rotateY(${rotateYValue}deg) scale(${scaleValue})`,
        transformStyle: 'preserve-3d',
        transition: 'transform 0.1s ease'
      }"
    >
      <img
        :src="imageSrc"
        :alt="altText"
        class="absolute top-0 left-0 object-cover rounded-[15px] will-change-transform"
        :style="{
          width: imageWidth,
          height: imageHeight,
          transform: 'translateZ(0)'
        }"
      />
      
      <div
        v-if="displayOverlayContent || $slots.overlay"
        class="absolute top-0 left-0 w-full h-full z-[2] will-change-transform"
        :style="{
          transform: 'translateZ(30px)'
        }"
      >
        <slot name="overlay"></slot>
      </div>
    </div>
    
    <div
      v-if="showTooltip"
      class="pointer-events-none absolute left-0 top-0 rounded-[4px] bg-white px-[10px] py-[4px] text-[10px] text-[#2d2d2d] z-[3] hidden sm:block"
      :style="{
        opacity: opacityValue,
        transform: `translate(${xPos}px, ${yPos}px) rotate(${rotateFigcaptionValue}deg)`,
        transition: 'opacity 0.2s ease'
      }"
    >
      {{ captionText }}
    </div>
  </figure>
</template>

<script setup>
import { ref, reactive, computed, onMounted, onUnmounted } from 'vue';

// Props definition
const props = defineProps({
  imageSrc: {
    type: String,
    required: true
  },
  altText: {
    type: String,
    default: 'Tilted card image'
  },
  captionText: {
    type: String,
    default: ''
  },
  containerHeight: {
    type: String,
    default: '300px'
  },
  containerWidth: {
    type: String,
    default: '100%'
  },
  imageHeight: {
    type: String,
    default: '300px'
  },
  imageWidth: {
    type: String,
    default: '300px'
  },
  scaleOnHover: {
    type: Number,
    default: 1.1
  },
  rotateAmplitude: {
    type: Number,
    default: 14
  },
  showMobileWarning: {
    type: Boolean,
    default: true
  },
  showTooltip: {
    type: Boolean,
    default: true
  },
  overlayContent: {
    type: [Object, String],
    default: null
  },
  displayOverlayContent: {
    type: Boolean,
    default: false
  }
});

// Refs
const cardRef = ref(null);
const lastY = ref(0);

// Animation values with spring-like behavior
const state = reactive({
  rotateX: 0,
  rotateY: 0,
  scale: 1,
  opacity: 0,
  rotateFigcaption: 0,
  x: 0,
  y: 0
});

// Spring animation targets
const springState = reactive({
  rotateX: 0,
  rotateY: 0,
  scale: 1,
  opacity: 0,
  rotateFigcaption: 0
});

// Computed values with spring animation
const rotateXValue = computed(() => {
  return springState.rotateX * 0.85 + state.rotateX * 0.15;
});

const rotateYValue = computed(() => {
  return springState.rotateY * 0.85 + state.rotateY * 0.15;
});

const scaleValue = computed(() => {
  return springState.scale * 0.9 + state.scale * 0.1;
});

const opacityValue = computed(() => {
  return springState.opacity;
});

const rotateFigcaptionValue = computed(() => {
  return springState.rotateFigcaption * 0.85 + state.rotateFigcaption * 0.15;
});

const xPos = computed(() => state.x);
const yPos = computed(() => state.y);

// Animation frame for spring physics
let animationFrame = null;

const updateSpringValues = () => {
  const springConfig = {
    damping: 30,
    stiffness: 100,
    mass: 2
  };
  
  const figcaptionSpringConfig = {
    damping: 30,
    stiffness: 350,
    mass: 1
  };
  
  // Apply spring physics for each value
  springState.rotateX += (state.rotateX - springState.rotateX) / springConfig.mass * springConfig.stiffness / 1000;
  springState.rotateX *= 1 - springConfig.damping / 100;
  
  springState.rotateY += (state.rotateY - springState.rotateY) / springConfig.mass * springConfig.stiffness / 1000;
  springState.rotateY *= 1 - springConfig.damping / 100;
  
  springState.scale += (state.scale - springState.scale) / springConfig.mass * springConfig.stiffness / 1000;
  springState.scale *= 1 - springConfig.damping / 100;
  
  springState.opacity += (state.opacity - springState.opacity) / 1 * 200 / 1000;
  
  springState.rotateFigcaption += (state.rotateFigcaption - springState.rotateFigcaption) / figcaptionSpringConfig.mass * figcaptionSpringConfig.stiffness / 1000;
  springState.rotateFigcaption *= 1 - figcaptionSpringConfig.damping / 100;
  
  animationFrame = requestAnimationFrame(updateSpringValues);
};

// Mouse event handlers
function handleMouse(e) {
  if (!cardRef.value) return;
  
  const rect = cardRef.value.getBoundingClientRect();
  const offsetX = e.clientX - rect.left - rect.width / 2;
  const offsetY = e.clientY - rect.top - rect.height / 2;
  
  // Update rotation values
  state.rotateX = (offsetY / (rect.height / 2)) * -props.rotateAmplitude;
  state.rotateY = (offsetX / (rect.width / 2)) * props.rotateAmplitude;
  
  // Update tooltip position
  state.x = e.clientX - rect.left;
  state.y = e.clientY - rect.top;
  
  // Calculate and apply figcaption rotation
  const velocityY = offsetY - lastY.value;
  state.rotateFigcaption = -velocityY * 0.6;
  lastY.value = offsetY;
}

function handleMouseEnter() {
  state.scale = props.scaleOnHover;
  state.opacity = 1;
}

function handleMouseLeave() {
  state.opacity = 0;
  state.scale = 1;
  state.rotateX = 0;
  state.rotateY = 0;
  state.rotateFigcaption = 0;
}

// Start animation loop on mount
onMounted(() => {
  updateSpringValues();
});

// Clean up animation frame on unmount
onUnmounted(() => {
  if (animationFrame) {
    cancelAnimationFrame(animationFrame);
  }
});
</script>