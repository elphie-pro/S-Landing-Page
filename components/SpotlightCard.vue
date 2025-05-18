<template>
  <div
    ref="divRef"
    @mousemove="handleMouseMove"
    @focus="handleFocus"
    @blur="handleBlur"
    @mouseenter="handleMouseEnter"
    @mouseleave="handleMouseLeave"
    class="relative rounded-3xl border border-neutral-800 bg-neutral-900 overflow-hidden p-8"
    :class="className"
  >
    <div
      class="pointer-events-none absolute inset-0 opacity-0 transition-opacity duration-500 ease-in-out"
      :style="{
        opacity,
        background: `radial-gradient(circle at ${position.x}px ${position.y}px, ${spotlightColor}, transparent 80%)`,
      }"
    />
    <slot></slot>
  </div>
</template>

<script setup>
import { ref, reactive, toRefs } from 'vue';

const props = defineProps({
  className: {
    type: String,
    default: '',
  },
  spotlightColor: {
    type: String,
    default: 'rgba(255, 255, 255, 0.25)',
  },
});

const divRef = ref(null);
const isFocused = ref(false);
const state = reactive({
  position: { x: 0, y: 0 },
  opacity: 0,
});

const { position, opacity } = toRefs(state);

const handleMouseMove = (e) => {
  if (!divRef.value || isFocused.value) return;
  const rect = divRef.value.getBoundingClientRect();
  position.value = { 
    x: e.clientX - rect.left, 
    y: e.clientY - rect.top 
  };
};

const handleFocus = () => {
  isFocused.value = true;
  opacity.value = 0.6;
};

const handleBlur = () => {
  isFocused.value = false;
  opacity.value = 0;
};

const handleMouseEnter = () => {
  opacity.value = 0.6;
};

const handleMouseLeave = () => {
  opacity.value = 0;
};
</script>