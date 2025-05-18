<template>
  <span
    :class="['flex flex-wrap relative', mainClassName]"
    ref="textContainerRef"
  >
    <!-- Screen-reader only text -->
    <span class="sr-only">{{ texts[currentTextIndex] }}</span>

    <div 
      class="relative w-full h-full overflow-hidden"
      aria-hidden="true"
    >
      <transition-group 
        name="text-rotate"
        tag="div"
      >
        <div
          v-if="showCurrentText"
          :key="currentTextIndex"
          class="w-full"
        >
          <template v-for="(wordObj, wordIndex) in elements" :key="`word-${wordIndex}`">
            <span 
              class="inline-flex"
              :class="splitLevelClassName"
            >
              <span 
                v-for="(char, charIndex) in wordObj.characters" 
                :key="`char-${charIndex}`"
                class="inline-block transition-all duration-500"
                :class="elementLevelClassName"
                :style="getCharacterStyle(wordIndex, charIndex)"
              >
                {{ char }}
              </span>
              <span v-if="wordObj.needsSpace" class="whitespace-pre"> </span>
            </span>
          </template>
        </div>
      </transition-group>
    </div>
  </span>
</template>

<script setup>
import { ref, computed, watch, onMounted, onBeforeUnmount } from 'vue'

const props = defineProps({
  texts: {
    type: Array,
    required: true,
    default: () => []
  },
  rotationInterval: {
    type: Number,
    default: 2000
  },
  staggerDuration: {
    type: Number,
    default: 0
  },
  staggerFrom: {
    type: [String, Number],
    default: 'first'
  },
  loop: {
    type: Boolean,
    default: true
  },
  auto: {
    type: Boolean,
    default: true
  },
  splitBy: {
    type: String,
    default: 'characters'
  },
  mainClassName: {
    type: String,
    default: ''
  },
  splitLevelClassName: {
    type: String,
    default: ''
  },
  elementLevelClassName: {
    type: String,
    default: ''
  }
})

const emit = defineEmits(['next'])

const currentTextIndex = ref(0)
const showCurrentText = ref(true)
const textContainerRef = ref(null)
let intervalId = null

// Split text into characters
const splitIntoCharacters = (text) => {
  if (typeof Intl !== "undefined" && Intl.Segmenter) {
    const segmenter = new Intl.Segmenter("en", { granularity: "grapheme" })
    return Array.from(segmenter.segment(text), (segment) => segment.segment)
  }
  return Array.from(text)
}

// Compute elements based on current text and split method
const elements = computed(() => {
  if (!props.texts[currentTextIndex.value]) return []
  
  const currentText = props.texts[currentTextIndex.value]
  
  if (props.splitBy === "characters") {
    const words = currentText.split(" ")
    return words.map((word, i) => ({
      characters: splitIntoCharacters(word),
      needsSpace: i !== words.length - 1,
    }))
  }
  if (props.splitBy === "words") {
    return currentText.split(" ").map((word, i, arr) => ({
      characters: [word],
      needsSpace: i !== arr.length - 1,
    }))
  }
  if (props.splitBy === "lines") {
    return currentText.split("\n").map((line, i, arr) => ({
      characters: [line],
      needsSpace: i !== arr.length - 1,
    }))
  }
  // For a custom separator
  return currentText.split(props.splitBy).map((part, i, arr) => ({
    characters: [part],
    needsSpace: i !== arr.length - 1,
  }))
})

// Get total character count for stagger calculations
const getTotalCharCount = computed(() => {
  return elements.value.reduce((sum, word) => sum + word.characters.length, 0)
})

// Helper function to get absolute character index
const getCharIndex = (wordIndex, charIndex) => {
  let previousCharsCount = 0
  for (let i = 0; i < wordIndex; i++) {
    previousCharsCount += elements.value[i]?.characters.length || 0
  }
  return previousCharsCount + charIndex
}

// Calculate stagger delay based on character position
const getStaggerDelay = (index) => {
  const total = getTotalCharCount.value
  if (props.staggerFrom === "first") return index * props.staggerDuration
  if (props.staggerFrom === "last") return (total - 1 - index) * props.staggerDuration
  if (props.staggerFrom === "center") {
    const center = Math.floor(total / 2)
    return Math.abs(center - index) * props.staggerDuration
  }
  if (props.staggerFrom === "random") {
    const randomIndex = Math.floor(Math.random() * total)
    return Math.abs(randomIndex - index) * props.staggerDuration
  }
  return Math.abs(props.staggerFrom - index) * props.staggerDuration
}

const getCharacterStyle = (wordIndex, charIndex) => {
  const index = getCharIndex(wordIndex, charIndex)
  const delay = getStaggerDelay(index)
  return {
    transitionDelay: `${delay}s`,
    opacity: 1,
    transform: 'translateY(0)'
  }
}

// Navigation methods
const handleIndexChange = (newIndex) => {
  // First hide current text
  showCurrentText.value = false
  
  // Wait for animation to complete before changing text
  setTimeout(() => {
    currentTextIndex.value = newIndex
    emit('next', newIndex)
    
    // Show new text with slight delay
    setTimeout(() => {
      showCurrentText.value = true
    }, 50)
  }, 500) // Match the CSS transition duration
}

const next = () => {
  const nextIndex =
    currentTextIndex.value === props.texts.length - 1
      ? props.loop
        ? 0
        : currentTextIndex.value
      : currentTextIndex.value + 1
  if (nextIndex !== currentTextIndex.value) {
    handleIndexChange(nextIndex)
  }
}

const previous = () => {
  const prevIndex =
    currentTextIndex.value === 0
      ? props.loop
        ? props.texts.length - 1
        : currentTextIndex.value
      : currentTextIndex.value - 1
  if (prevIndex !== currentTextIndex.value) {
    handleIndexChange(prevIndex)
  }
}

const jumpTo = (index) => {
  const validIndex = Math.max(0, Math.min(index, props.texts.length - 1))
  if (validIndex !== currentTextIndex.value) {
    handleIndexChange(validIndex)
  }
}

const reset = () => {
  if (currentTextIndex.value !== 0) {
    handleIndexChange(0)
  }
}

// Setup auto-rotation
const startInterval = () => {
  clearInterval(intervalId)
  if (props.auto && props.texts.length > 1) {
    intervalId = setInterval(next, props.rotationInterval)
  }
}

watch(() => props.auto, startInterval)
watch(() => props.rotationInterval, startInterval)
watch(() => props.texts, startInterval, { deep: true })

onMounted(() => {
  startInterval()
  // Initialize with visible text
  showCurrentText.value = true
})

onBeforeUnmount(() => {
  clearInterval(intervalId)
})

// Expose methods to parent components
defineExpose({
  next,
  previous,
  jumpTo,
  reset
})
</script>

<style scoped>
.text-rotate-enter-active,
.text-rotate-leave-active {
  transition: all 0.5s ease;
}

.text-rotate-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.text-rotate-leave-to {
  opacity: 0;
  transform: translateY(-20px);
  position: absolute;
}

.text-rotate-enter-from .inline-block,
.text-rotate-leave-to .inline-block {
  opacity: 0;
  transform: translateY(100%);
}
</style>