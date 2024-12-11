<template>
    <div class="flex space-x-2 items-center">
        <div
            class="text-gray-500 text-xs"
            v-if="showNextModeLabel"
        >
            Change to {{ nextMode }}
        </div>
        <button
            @click="toggleMode"
            @mouseenter="showNextModeLabel = true"
            @mouseleave="showNextModeLabel = false"
            class="hover:bg-gray-200 dark:hover:bg-gray-600 px-2 py-1 text-gray-500 rounded"
        >
            {{ nextModeIcon }}
        </button>
    </div>
</template>

<script setup>
const showNextModeLabel = ref(false);
const colorMode = useColorMode();

// Available color modes
const modes = ["system", "light", "dark"];

// Set the next mode icons
const nextModeIcons = {
    system: "🌓",
    light: "🌕",
    dark: "🌑",
};

// Get the next color mode
const nextMode = computed(() => {
    const currentModeIndex = modes.indexOf(colorMode.preference);
    let nextModeIndex = null;

    if (currentModeIndex + 1 === modes.length) {
        nextModeIndex = 0;
    } else {
        nextModeIndex = currentModeIndex + 1;
    }

    return modes[nextModeIndex];
});

// Get the next mode icon
const nextModeIcon = computed(() => nextModeIcons[nextMode.value]);

// Toggle the color mode
const toggleMode = () => {
    colorMode.preference = nextMode.value;
};
</script>
