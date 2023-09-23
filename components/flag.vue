<template>
    <div>
        <li class="w-full">
            <img :src="info.flags.svg" :alt="info.name.common" lazy class="rounded-r-3xl">
            <span>
                name : {{ info.name.common }}
                continent : {{ info.continents[0] }}
            </span>
        </li>
    </div>
</template>

<script setup>
defineProps({
    info: Object,
})

const result = await $fetch('https://restcountries.com/v3.1/all').catch((error) => error.data)

</script>

<style>
.flag {
    @apply bg-white block w-[18%] p-2 border m-2
}

.flag img {
    height: 150px;
}
</style>