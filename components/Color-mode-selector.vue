<template>
    <div class="flex space-x-2 items-center">
        <div class="text-gray-500 text-xs" v-if="showNextModeLabel">Chage to {{ nextMode }}</div>
        <button @click="toggleMode" @mouseenter="showNextModeLabel = true" 
            class="hover:bg-gray-200 dark:hover:bg-gray-600 px-2 py-1 test-gray-500">{{ nextModeIcon }}
        </button>
    </div>  
</template>

<script setup lang="ts">
const showNextModeLabel = ref(false)
const colorMode = useColorMode()

type Mode = 'system'|'light'|'dark';

const modes: Mode[] = [
    'system',
    'light',
    'dark'
]

const nextModeIcons: Record<Mode, string> = {
  system: '🌓',
  light: '🌕',
  dark: '🌑'
}


const nextMode = computed(() => {

    const currentModeIndex = modes.indexOf(colorMode.preference as Mode)
    let nextModeIndex = null

    if ( currentModeIndex + 1 === modes.length){
        nextModeIndex = 0
    } else {
        nextModeIndex = currentModeIndex + 1
    }
    return modes[nextModeIndex]
})

const nextModeIcon = computed(() => nextModeIcons[nextMode.value])
const toggleMode = () => colorMode.preference = nextMode.value
</script>