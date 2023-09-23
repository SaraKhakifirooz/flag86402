<template>
    <div class="border p-3 bg-gray-100 my-3">
        My Form
        <label v-if="label" :for="id">{{ label }}</label>
        <input v-model="localModelValue" :name="name" :id="id" :type="type" />
        <br>
        localModelValue {{ localModelValue }}
    </div>
</template>

<script setup>
import { string, oneOfType, bool, number } from 'vue-types'

const props = defineProps({
    label: string(),
    id: string(),
    name: string(),
    type: string().def('text'),
    modelValue: oneOfType([string(), number(), bool()])
})

const { localModelValue } = useLocalModelValue({ props })

</script>