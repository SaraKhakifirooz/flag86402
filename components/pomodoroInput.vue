<template>
    <div>
        <br />
        <div class="grid">
            <label :for="id">{{ label }}</label>
            <input v-model="localModelValue" :name="name" :id="id" :type="type" class="border">
        </div>
        <br />

    </div>
</template>

<script setup>
import { string, oneOfType, number } from 'vue-types'

const props = defineProps({
    label: string(),
    id: string(),
    name: string(),
    type: string().def('text'),
    modelValue: oneOfType([string(), number()])
})


const { localModelValue } = useLocalModelValue({ props })


// validateEmail(email) {
//     if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(email)) {
//         return
//     } else {
//         alert("Email invalid!")
//     }
// }


</script>