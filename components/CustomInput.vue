
<script setup>
defineProps(['modelValue'])
defineEmits(['update:modelValue'])
</script>

<template>
    <div class="border p-3 bg-gray-00 my-3">
        <h1>Custom Input</h1>

        <input class="border"
        :value="modelValue" 
        @input="$emit('update:modelValue', $event.target.value)" />

    </div>
</template>