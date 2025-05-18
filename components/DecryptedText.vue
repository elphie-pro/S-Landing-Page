<template>
  <span
    ref="containerRef"
    class="inline-block whitespace-pre-wrap"
    :class="parentClassName"
    v-motion
    :initial="{ opacity: 1 }"
    v-bind="$attrs"
    @mouseenter="animateOn === 'hover' && startHovering()"
    @mouseleave="animateOn === 'hover' && stopHovering()"
  >
    <span class="sr-only">{{ displayText }}</span>

    <span aria-hidden="true">
      <span
        v-for="(char, index) in displayText.split('')"
        :key="index"
        :class="isRevealedOrDone(index) ? className : encryptedClassName"
      >
        {{ char }}
      </span>
    </span>
  </span>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted, watch } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'

const props = defineProps({
  text: {
    type: String,
    required: true
  },
  speed: {
    type: Number,
    default: 50
  },
  maxIterations: {
    type: Number,
    default: 10
  },
  sequential: {
    type: Boolean,
    default: false
  },
  revealDirection: {
    type: String,
    default: 'start',
    validator: (value) => ['start', 'end', 'center'].includes(value)
  },
  useOriginalCharsOnly: {
    type: Boolean,
    default: false
  },
  characters: {
    type: String,
    default: 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz!@#$%^&*()_+'
  },
  className: {
    type: String,
    default: ''
  },
  parentClassName: {
    type: String,
    default: ''
  },
  encryptedClassName: {
    type: String,
    default: ''
  },
  animateOn: {
    type: String,
    default: 'hover',
    validator: (value) => ['hover', 'view'].includes(value)
  }
})

const displayText = ref(props.text)
const isHovering = ref(false)
const isScrambling = ref(false)
const revealedIndices = ref(new Set())
const hasAnimated = ref(false)
const containerRef = ref(null)
let interval = null
let currentIteration = 0

const availableChars = computed(() => {
  if (props.useOriginalCharsOnly) {
    return Array.from(new Set(props.text.split(''))).filter(char => char !== ' ')
  }
  return props.characters.split('')
})

const isRevealedOrDone = (index) => {
  return revealedIndices.value.has(index) || !isScrambling.value || !isHovering.value
}

const getNextIndex = (revealedSet) => {
  const textLength = props.text.length
  switch (props.revealDirection) {
    case 'start':
      return revealedSet.size
    case 'end':
      return textLength - 1 - revealedSet.size
    case 'center': {
      const middle = Math.floor(textLength / 2)
      const offset = Math.floor(revealedSet.size / 2)
      const nextIndex =
        revealedSet.size % 2 === 0
          ? middle + offset
          : middle - offset - 1

      if (nextIndex >= 0 && nextIndex < textLength && !revealedSet.has(nextIndex)) {
        return nextIndex
      }
      for (let i = 0; i < textLength; i++) {
        if (!revealedSet.has(i)) return i
      }
      return 0
    }
    default:
      return revealedSet.size
  }
}

const shuffleText = (originalText, currentRevealed) => {
  if (props.useOriginalCharsOnly) {
    const positions = originalText.split('').map((char, i) => ({
      char,
      isSpace: char === ' ',
      index: i,
      isRevealed: currentRevealed.has(i)
    }))

    const nonSpaceChars = positions
      .filter(p => !p.isSpace && !p.isRevealed)
      .map(p => p.char)

    for (let i = nonSpaceChars.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1))
      ;[nonSpaceChars[i], nonSpaceChars[j]] = [nonSpaceChars[j], nonSpaceChars[i]]
    }

    let charIndex = 0
    return positions
      .map(p => {
        if (p.isSpace) return ' '
        if (p.isRevealed) return originalText[p.index]
        return nonSpaceChars[charIndex++]
      })
      .join('')
  } else {
    return originalText
      .split('')
      .map((char, i) => {
        if (char === ' ') return ' '
        if (currentRevealed.has(i)) return originalText[i]
        return availableChars.value[Math.floor(Math.random() * availableChars.value.length)]
      })
      .join('')
  }
}

const startScrambling = () => {
  isScrambling.value = true
  
  interval = setInterval(() => {
    if (props.sequential) {
      if (revealedIndices.value.size < props.text.length) {
        const nextIndex = getNextIndex(revealedIndices.value)
        const newRevealed = new Set(revealedIndices.value)
        newRevealed.add(nextIndex)
        revealedIndices.value = newRevealed
        displayText.value = shuffleText(props.text, newRevealed)
      } else {
        clearInterval(interval)
        isScrambling.value = false
      }
    } else {
      displayText.value = shuffleText(props.text, revealedIndices.value)
      currentIteration++
      if (currentIteration >= props.maxIterations) {
        clearInterval(interval)
        isScrambling.value = false
        displayText.value = props.text
      }
    }
  }, props.speed)
}

const startHovering = () => {
  isHovering.value = true
}

const stopHovering = () => {
  isHovering.value = false
  displayText.value = props.text
  revealedIndices.value = new Set()
  isScrambling.value = false
  if (interval) {
    clearInterval(interval)
  }
}

watch(isHovering, (newValue) => {
  if (newValue) {
    currentIteration = 0
    startScrambling()
  } else {
    stopHovering()
  }
})

// Set up intersection observer for view-triggered animation
onMounted(() => {
  if (props.animateOn === 'view') {
    const observer = useIntersectionObserver(containerRef, ([{ isIntersecting }]) => {
      if (isIntersecting && !hasAnimated.value) {
        isHovering.value = true
        hasAnimated.value = true
      }
    }, { threshold: 0.1 })
  }
})

// Clean up on component unmount
onUnmounted(() => {
  if (interval) {
    clearInterval(interval)
  }
})

// Update displayText when text prop changes
watch(() => props.text, (newText) => {
  displayText.value = newText
})
</script>